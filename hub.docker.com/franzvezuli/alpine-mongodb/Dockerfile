FROM alpine:3.9

# Don't need to specify a version. There is only one entry for mongodb in Alpine Linux v3.9: 4.0.5-r0
# https://pkgs.alpinelinux.org/packages?name=mongodb&branch=v3.9&arch=x86_64
RUN apk add --no-cache mongodb

# This is the default directory for the MongoDB database
VOLUME /data/db

# 27017 is the default recommended mongodb port, but we'll expose 1 more as well just in case.
EXPOSE 27017 27018

# Runs our shell script, mainly to set owner of the directories and run mongod under the mongodb user
COPY docker-entrypoint.sh /
ENTRYPOINT ["/docker-entrypoint.sh"]
