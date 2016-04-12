FROM postgres:9.5
MAINTAINER Javi Palanca <jpalanca@gmail.com>

ENV POSTGIS_MAJOR 2.2
ENV POSTGIS_VERSION 2.2.2+dfsg-1.pgdg80+1

RUN apt-get update \
      && apt-get install -y --no-install-recommends --force-yes \
           postgresql-$PG_MAJOR-postgis-$POSTGIS_MAJOR=$POSTGIS_VERSION \
           postgis=$POSTGIS_VERSION \
           git \
           build-essential \
           libpq-dev \
           postgresql-server-dev-9.5 \
      && rm -rf /var/lib/apt/lists/*

RUN mkdir -p /code
WORKDIR /code
RUN git config --global http.sslVerify false
RUN git clone http://github.com/umitanuki/kmeans-postgresql.git
WORKDIR /code/kmeans-postgresql
RUN make
RUN make install

RUN mkdir -p /docker-entrypoint-initdb.d
COPY ./initdb-postgis.sh /docker-entrypoint-initdb.d/postgis.sh
