# shoifele/nodejs-media

FROM shoifele/nodejs

MAINTAINER Christoph Wiechert <wio@psitrax.de>

ENV REFRESHED_AT="2015-10-31"

## install anything we need in one turn
RUN apt-get update && \
  apt-get install -y --no-install-recommends \
    graphicsmagick libav-tools libavcodec-extra libavcodec-extra-56 && \
  apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* /build;

CMD ["/init"]
