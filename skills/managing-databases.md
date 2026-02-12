# Managing Databases

Guides database architecture decisions for PostgreSQL, DuckDB, Parquet, and PGVector. Use when designing schemas, choosing storage strategies, optimizing queries, or diagnosing performance issues.

## When to Use Which

| Workload | Use | Why |
|----------|-----|-----|
| Transactional (CRUD, users, sessions) | PostgreSQL | ACID, row-level locking, indexes |
| Analytical (aggregations, scans) | DuckDB | Columnar, vectorized, parallel |
| Data storage/interchange | Parquet | Compressed, columnar, portable |
| Metadata + relationships | PostgreSQL | Foreign keys, constraints |
| Ad-hoc exploration | DuckDB | Fast on Parquet, no ETL needed |
| Time-series with point lookups | PostgreSQL + partitioning | Partition pruning + indexes |
| Time-series analytics | DuckDB on Parquet | Scan performance |
| Vector similarity search | PostgreSQL + PGVector | HNSW/IVFFlat indexes, hybrid search |
| RAG / semantic search | PostgreSQL + PGVector | Embeddings + metadata in same DB |

## PostgreSQL Quick Reference

**Use for:** Metadata, relationships, OLTP workloads, anything needing ACID.

**Key decisions:**
- Partition tables >100M rows or with retention requirements
- Index columns in WHERE/JOIN clauses, not everything
- Tune autovacuum for high-churn tables

**Query optimization:**
```sql
-- Always check query plans
EXPLAIN (ANALYZE, BUFFERS) SELECT ...

-- Partial indexes for common filters
CREATE INDEX idx_active_users ON users(email) WHERE active = true;

-- Use CTEs for readability, but know they're optimization fences in older PG
```

## DuckDB Quick Reference

**Use for:** Analytics, aggregations, Parquet queries, data exploration.

**Key decisions:**
- Prefer Parquet files over CSV (10-100x faster)
- Let DuckDB auto-parallelize; don't micro-optimize
- For remote data, increase threads beyond CPU count

```sql
-- Query Parquet directly
SELECT * FROM read_parquet('data/*.parquet') WHERE year >= 2020;

-- Aggregate across files
SELECT region, SUM(revenue) FROM read_parquet('sales/**/*.parquet')
GROUP BY region ORDER BY 2 DESC;
```

## Parquet Quick Reference

**Use for:** Storing analytical data, data interchange, columnar compression.

**Key decisions:**
- Target 128MB-1GB file sizes
- Partition by low-to-moderate cardinality columns (date, region)
- Sort by columns used in filters for better pruning

## PGVector Quick Reference

**Use for:** Similarity search, RAG, semantic search, recommendations.

**Key decisions:**
- HNSW for low-latency, high-recall (default choice)
- IVFFlat for memory-constrained or batch-updated data
- Use iterative scan for filtered queries
- Consider hybrid search (vector + keyword) for 8-15% accuracy boost

```sql
-- Create vector column
ALTER TABLE documents ADD COLUMN embedding vector(1536);

-- HNSW index
CREATE INDEX ON documents USING hnsw (embedding vector_cosine_ops);

-- Similarity search
SELECT * FROM documents ORDER BY embedding <=> $1 LIMIT 10;

-- Hybrid search (vector + keyword)
SELECT *, (0.7 * vector_score + 0.3 * text_score) AS combined
FROM ...
```

## Cross-Database Conventions

### Naming
- snake_case tables and columns
- Singular table names (`dataset` not `datasets`)
- Timestamps: always UTC, use `TIMESTAMPTZ` in PostgreSQL

### Normalization Decisions

| Pattern | When to normalize | When to denormalize |
|---------|-------------------|---------------------|
| Lookup tables | PostgreSQL, changes frequently | DuckDB/Parquet, static data |
| Repeated values | PostgreSQL, storage matters | Parquet, compression handles it |
| Joins at query time | PostgreSQL, complex relationships | Parquet, pre-join for analytics |

## Performance Debugging

### PostgreSQL Slow Query
1. Run `EXPLAIN (ANALYZE, BUFFERS)`
2. Check for sequential scans on large tables
3. Verify indexes on filter/join columns
4. Check `pg_stat_user_tables` for bloat
5. Review `work_mem` if seeing disk sorts

### DuckDB Slow Query
1. Check if reading CSV instead of Parquet
2. Verify not doing `SELECT *` on remote data
3. Check thread count
4. Look for unnecessary type conversions

### Parquet Slow Reads
1. Verify predicate pushdown is working
2. Check file sizes (too small = overhead, too large = no parallelism)
3. Confirm data sorted by filter columns
4. Look for high-cardinality partition keys

### PGVector Slow Search
1. Verify index exists and is being used
2. Check `ef_search` (HNSW) or `probes` (IVFFlat) settings
3. Enable iterative scan for filtered queries
4. Consider partial indexes for common filters
