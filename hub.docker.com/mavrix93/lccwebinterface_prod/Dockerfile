FROM ubuntu:14.04

MAINTAINER Martin Vo

ENV TINI_VERSION v0.14.0
ADD https://github.com/krallin/tini/releases/download/${TINI_VERSION}/tini /tini
RUN chmod +x /tini
ENTRYPOINT ["/tini", "--"]

# install all system requirements for the first layer
RUN set -ex \
    && apt-get update && apt-get -y upgrade \
    && apt-get install -y python python-pip python-dev python-tk \
    libfreetype6-dev libpng12-dev libxft-dev libblas-dev liblapack-dev libatlas-base-dev gfortran nginx dialog net-tools \
    libxml2-dev libxslt1-dev python-lxml

# Set env variables used in this Dockerfile (add a unique prefix, such as DOCKYARD)
ENV DOCKYARD_SRC=web \
    DOCKYARD_SRVHOME=/srv
ENV DOCKYARD_SRVPROJ=$DOCKYARD_SRVHOME/web \
    DOCKYARD_SRVDATA=$DOCKYARD_SRVHOME/data \
    DOCKYARD_SRVSAMPLE=$DOCKYARD_SRVHOME/sample_data \
    DOCKYARD_SRVLOGS=$DOCKYARD_SRVHOME/logs \
    DOCKYARD_SRVSTATIC=$DOCKYARD_SRVHOME/static/ \
    DOCKYARD_WORKERS=3 \
    DOCKYARD_PORT=8000 \
    DOCKYARD_APP_CONTEXT=lcc \
    MPLBACKEND="agg"
    #DOCKYARD_SECRET - should be set during deployment

# prepare web application
ADD $DOCKYARD_SRC $DOCKYARD_SRVPROJ
ADD sample_data $DOCKYARD_SRVSAMPLE

RUN pip install --upgrade pip
RUN mkdir -p $DOCKYARD_SRVSTATIC $DOCKYARD_SRVLOGS \
    && pip install -r $DOCKYARD_SRVPROJ/requirements.txt

# prepare nginx configuration
ADD nginx.conf /etc/nginx/sites-enabled/default

# Port to expose
EXPOSE 80
# 'data' folder for user outputs (better to store data on external ftp
VOLUME ["$DOCKYARD_SRVDATA", "$DOCKYARD_SRVLOGS"]

WORKDIR $DOCKYARD_SRVPROJ
COPY ./docker-entrypoint.sh /
RUN chmod +x /docker-entrypoint.sh
CMD "/docker-entrypoint.sh"
