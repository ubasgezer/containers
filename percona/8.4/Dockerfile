ARG PERCONA_VERSION=8.4
FROM percona/percona-server:${PERCONA_VERSION}

ENV MYSQL_ALLOW_EMPTY_PASSWORD=1
ENV PERCONA_TELEMETRY_DISABLE=1

RUN echo "[mysqld]" > /etc/my.cnf.d/custom.cnf \
    && echo "sql_mode=STRICT_ALL_TABLES,NO_ZERO_IN_DATE,ERROR_FOR_DIVISION_BY_ZERO,NO_ENGINE_SUBSTITUTION" >> /etc/my.cnf.d/custom.cnf \
    && echo "collation_server=utf8mb4_unicode_ci" >> /etc/my.cnf.d/custom.cnf \
    && echo "character_set_server=utf8mb4" >> /etc/my.cnf.d/custom.cnf \
    && echo "explicit_defaults_for_timestamp=ON" >> /etc/my.cnf.d/custom.cnf \
    && echo "binlog_expire_logs_seconds=864000" >> /etc/my.cnf.d/custom.cnf \
    && echo "binlog_space_limit=10G" >> /etc/my.cnf.d/custom.cnf \
    && echo "max_binlog_size=100M" >> /etc/my.cnf.d/custom.cnf \
    && echo "innodb_flush_log_at_trx_commit=0" >> /etc/my.cnf.d/custom.cnf \
    && echo "max_allowed_packet=64M" >> /etc/my.cnf.d/custom.cnf
