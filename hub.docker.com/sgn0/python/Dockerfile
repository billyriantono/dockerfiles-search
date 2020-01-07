FROM sgn0/baseimage
MAINTAINER Jesus Lopez, jesus@sgn.com

# python
RUN set -ex; \
    apk --no-cache -q add python; \
    find /usr/lib/python2.7 -name '*.py[co]' -print0 | xargs -0 rm

CMD ["/usr/bin/python"]
