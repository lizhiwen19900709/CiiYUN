FROM kobotoolbox/postgres_base:latest

# Copy over the config. files.
COPY pg_hba.conf postgresql.conf /etc/postgresql/9.4/main/

# Prepare the backups and Postgres cluster directories and initialize the cluster.
RUN mkdir -p /srv/backups/ /srv/db && \
    chown postgres:postgres /srv/db && \
    sudo -u postgres /usr/lib/postgresql/9.4/bin/initdb -D /srv/db -E utf-8 --locale=en_US.UTF-8

# Copy over run-time scripts.
COPY run_postgres /etc/service/postgres/run
COPY ./init_postgres.bash /etc/my_init.d/10_init_postgres.bash

VOLUME ["/srv/db", "/srv/backups/"]
EXPOSE 5432