FROM nerelohw/docker-alpine-abuild:3.8

ENV ALPINE_BRANCH main
COPY apkbuilds/$ALPINE_BRANCH $APKBUILDS/$ALPINE_BRANCH

## must keep $APKBUILDS clean
RUN abuild.sh --mode local --repository main --package mariadb
