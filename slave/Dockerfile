# To build image for this dockerfile use this command:
#   docker build -t terrabrasilis/postgres-slave -f slave/Dockerfile --no-cache .
#
# To run with compose use the command:
#   docker-compose -f docker-compose-slave.yml up
#
FROM postgres:9.6
LABEL author="Andre Carvalho" \
      project="TerraBrasilis"

ENV POSTGIS_MAJOR 2.4
ENV POSTGIS_VERSION 2.4.4+dfsg-4.pgdg90+1

RUN apt-get update \
      && apt-get install -y --no-install-recommends \
           postgresql-$PG_MAJOR-postgis-$POSTGIS_MAJOR=$POSTGIS_VERSION \
           postgresql-$PG_MAJOR-postgis-$POSTGIS_MAJOR-scripts=$POSTGIS_VERSION \
           postgis=$POSTGIS_VERSION \
      && apt-get install -y iputils-ping \
      && rm -rf /var/lib/apt/lists/*

ENV PG_MAX_WAL_SENDERS 8
ENV PG_WAL_KEEP_SEGMENTS 8
COPY setup-replication.sh /docker-entrypoint-initdb.d/
COPY docker-entrypoint.sh /docker-entrypoint.sh
RUN chmod +x /docker-entrypoint-initdb.d/setup-replication.sh /docker-entrypoint.sh
