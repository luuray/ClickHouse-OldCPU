ARG CLICKHOUSE_VERSION
FROM clickhouse/clickhouse-server:${CLICKHOUSE_VERSION}

ARG BUILD_DATE
ARG SOURCE_REVISION
ARG SOURCE_TAG

LABEL org.opencontainers.image.created="${BUILD_DATE}" \
      org.opencontainers.image.description="ClickHouse Server for x86-64-v2 CPUs without an AVX2 requirement" \
      org.opencontainers.image.licenses="Apache-2.0" \
      org.opencontainers.image.revision="${SOURCE_REVISION}" \
      org.opencontainers.image.source="https://github.com/luuray/ClickHouse-OldCPU" \
      org.opencontainers.image.title="ClickHouse OldCPU" \
      org.opencontainers.image.url="https://github.com/luuray/ClickHouse-OldCPU" \
      org.opencontainers.image.version="${SOURCE_TAG}"

USER root
COPY --chmod=0755 clickhouse /usr/bin/clickhouse

RUN clickhouse local --query "SELECT 1" | grep -qx 1
