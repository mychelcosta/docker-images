ARG PG_MAJOR
ARG VCHORD_TAG
ARG PGROONGA_TAG

FROM tensorchord/vchord-scratch:pg${PG_MAJOR}-v${VCHORD_TAG} AS vchord

FROM groonga/pgroonga:${PGROONGA_TAG}-debian-${PG_MAJOR}

ARG PG_MAJOR

RUN apt-get update && apt-get install -y --no-install-recommends \
    postgresql-${PG_MAJOR}-pgvector \
    postgresql-${PG_MAJOR}-cron \
 && rm -rf /var/lib/apt/lists/*

COPY --from=vchord / /

CMD ["postgres", \
     "-c", "cron.database_name=postgres", \
     "-c", "shared_preload_libraries=pg_cron,vchord", \
     "-c", "logging_collector=on"]