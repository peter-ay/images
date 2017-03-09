FROM webuni/base:3.5
MAINTAINER Martin Hasoň "martin.hason@gmail.com"

# group postgres already exists
#RUN addgroup -S postgres && adduser -S -G postgres postgres

RUN apk --update add postgresql postgresql-contrib \
    && rm -rf /var/cache/apk/* /tmp/*

# make the sample config easier to munge (and "correct by default")
RUN sed -ri "s!^#?(listen_addresses)\s*=\s*\S+.*!\1 = '*'!" /usr/share/postgresql/postgresql.conf.sample

RUN mkdir -p /var/run/postgresql && chown -R postgres:postgres /var/run/postgresql && chmod g+s /var/run/postgresql

RUN mkdir /docker-entrypoint-initdb.d

ENV LANG en_US.utf8
ENV PGDATA /var/lib/postgresql/data
RUN mkdir -p "$PGDATA" && chown -R postgres:postgres "$PGDATA" && chmod 777 "$PGDATA" # this 777 will be replaced by 700 at runtime (allows semi-arbitrary "--user" values)
VOLUME /var/lib/postgresql/data

COPY rootfs /

EXPOSE 5432

CMD [ "postgres" ]

# Dockerfile is based on https://github.com/docker-library/postgres/blob/master/9.6/alpine/Dockerfile