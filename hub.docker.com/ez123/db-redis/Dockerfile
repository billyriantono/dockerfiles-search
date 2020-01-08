# v1.0.1    2018-08-31     webmaster@highskillz.com
#
FROM redis:5.0-alpine

MAINTAINER HighSkillz <webdev@highskillz.com>

RUN apk add --no-cache --update \
        bash \
        coreutils \
        tini \
    && echo done...

ENTRYPOINT ["/sbin/tini", "--", "docker-entrypoint.sh"]
CMD ["redis-server"]
