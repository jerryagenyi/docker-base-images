FROM postgres:latest

# Install common PostgreSQL extensions and utilities
RUN apt-get update \
    && apt-get install -y --no-install-recommends \
        postgresql-contrib \
        postgis \
        pgcrypto \
        pg_stat_statements \
    && rm -rf /var/lib/apt/lists/*

# Default environment variables
ENV POSTGRES_USER=user \
    POSTGRES_PASSWORD=pass \
    POSTGRES_DB=mydb \
    # Optimized PostgreSQL configuration for development
    POSTGRES_INITDB_ARGS="--encoding=UTF-8 --lc-collate=C --lc-ctype=C" \
    POSTGRES_HOST_AUTH_METHOD=md5

# Create extensions setup script
RUN echo '\
CREATE EXTENSION IF NOT EXISTS "uuid-ossp";\n\
CREATE EXTENSION IF NOT EXISTS "hstore";\n\
CREATE EXTENSION IF NOT EXISTS "postgis";\n\
CREATE EXTENSION IF NOT EXISTS "pg_stat_statements";\n\
' > /docker-entrypoint-initdb.d/init-extensions.sql

# Custom PostgreSQL configuration
COPY <<-"EOT" /tmp/postgresql.conf
max_connections = 100
shared_buffers = 128MB
effective_cache_size = 512MB
work_mem = 8MB
maintenance_work_mem = 128MB
random_page_cost = 1.1
temp_file_limit = 10GB
log_min_duration_statement = 200ms
idle_in_transaction_session_timeout = 10s
lock_timeout = 1s
statement_timeout = 60s
shared_preload_libraries = 'pg_stat_statements'
pg_stat_statements.max = 10000
pg_stat_statements.track = all
EOT

RUN cat /tmp/postgresql.conf >> /usr/share/postgresql/postgresql.conf.sample

VOLUME /var/lib/postgresql/data
EXPOSE 5432