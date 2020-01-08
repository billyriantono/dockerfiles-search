FROM debian:jessie
MAINTAINER simon@simonluijk.com

RUN echo 'DPkg::Post-Invoke {"/bin/rm -f /var/cache/apt/archives/*.deb || true";};' | tee /etc/apt/apt.conf.d/no-cache && \
    apt-get update -y && \
    apt-get dist-upgrade -y && \
    apt-get clean && \
    rm -rf /var/cache/apt/* && \
    DEBIAN_FRONTEND=noninteractive apt-get install -y git python-pip \
        python-dev python-psycopg2 python-mysqldb
