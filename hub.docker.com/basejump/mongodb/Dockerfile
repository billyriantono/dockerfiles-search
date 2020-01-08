### Dockerfile
#
# Mongodb

FROM basejump/build-base
MAINTAINER Devon Weller <dweller@atlasworks.com>

ADD mongo.repo /etc/yum.repos.d/mongo.repo

RUN yum install -y mongodb-org-server

RUN mkdir -p /data/db

# Expose ports
EXPOSE 27017

# CMD  ["/usr/bin/mongod"]
# CMD  ["/usr/bin/mongod","--nojournal"]
CMD  ["/usr/bin/mongod","--smallfiles"]


