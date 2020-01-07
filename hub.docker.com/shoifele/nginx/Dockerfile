# shoifele/nginx

FROM shoifele/bone

MAINTAINER Sebastian Sauer <info@dynpages.de>
MAINTAINER Christoph Wiechert <wio@psitrax.de>

ENV REFRESHED_AT="2016-03-16"

# UID of www-data
# change to fix mount problems
ENV RUN_UID=33

# install anything we need in one turn
RUN apt-get update && \
  apt-get install -y --no-install-recommends nginx && \
  rm -rf /etc/nginx && \
  apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* /build;

ADD rootfs /

EXPOSE 80

VOLUME [ "/etc/nginx", "/var/log/nginx" ]

CMD ["/init"]
