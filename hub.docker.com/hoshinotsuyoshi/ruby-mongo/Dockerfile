FROM hoshinotsuyoshi/ruby

RUN apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv 7F0CEB10 && \
    echo 'deb http://downloads-distro.mongodb.org/repo/ubuntu-upstart dist 10gen' | tee /etc/apt/sources.list.d/10gen.list && \
    apt-get -y update && \
    apt-get -y install -q mongodb-org && \
    mkdir -p /data/db
# EXPOSE 27017
# ENTRYPOINT usr/bin/mongod
