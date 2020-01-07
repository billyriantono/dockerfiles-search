#
# Dockerfile
#
FROM mkovac/runit-stretch:latest
MAINTAINER Matej Kovac <matej.kovac@gmail.com>

# assets - big, pre-downloaded files, not modified very often
#
#COPY assets /root/assets

# files and scripts needed to build the image
#
COPY build /root/build

RUN run-parts --report --exit-on-error /root/build/scripts && \
  rm -rfv /root/build /root/assets

# if you need to mount builds...
VOLUME ["/home/gitlab-runner/data", "/home/gitlab-runner/builds" ]

# from parent...
#ENTRYPOINT ["/sbin/entrypoint.sh"]
# from parent...
#CMD ["/usr/bin/dumb-init", "/etc/rc.local"]
