FROM alvrme/alpine-android:android-28
MAINTAINER Younes Benaomar <younes@interactive-object.com>

RUN echo http://dl-cdn.alpinelinux.org/alpine/edge/main >> /etc/apk/repositories
RUN echo http://dl-cdn.alpinelinux.org/alpine/edge/community >> /etc/apk/repositories
RUN apk update && apk upgrade && apk add git nodejs-current npm yarn

RUN npm install appcenter-cli @sentry/cli semver -g --unsafe-perm
RUN echo fs.inotify.max_user_watches=524288 | tee -a /etc/sysctl.conf && sysctl -p

