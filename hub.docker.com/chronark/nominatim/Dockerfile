FROM golang AS compile_stage

WORKDIR /

COPY ./scripts/*.go ./
RUN  go mod init nominatim

RUN env GOOS=linux go build -o /wait /wait.go

FROM ubuntu:18.04

ENV DEBIAN_FRONTEND noninteractive
RUN apt-get -qq update && apt-get -qq upgrade -y \
    apache2 \
    build-essential \
    cmake \
    g++ \
    git \
    libapache2-mod-php \
    libboost-dev \
    libboost-filesystem-dev \
    libboost-system-dev \
    libbz2-dev \
    libexpat1-dev \
    libpq-dev \
    libproj-dev \
    libxml2-dev \
    php \
    php-intl \
    php-pgsql \
    postgresql-10-postgis-2.4 \
    postgresql-10-postgis-scripts \
    postgresql-contrib-10 \
    postgresql-server-dev-10 \
    zlib1g-dev 

WORKDIR /

RUN git clone --recursive https://github.com/openstreetmap/Nominatim ./src
WORKDIR /src/build
RUN cmake .. && make -j $(nproc)

COPY local.php /src/build/settings/
COPY nominatim.conf /etc/apache2/conf-available/



RUN a2enconf nominatim

COPY ./scripts /scripts
COPY --from=compile_stage /wait /wait

CMD /wait ${DB_HOST} ${DB_PORT} 60 && /usr/sbin/apache2ctl -D FOREGROUND