# tkdiff in a container
#
# docker run  --rm \
#        -v /tmp/.X11-unix:/tmp/.X11-unix \
#        -e DISPLAY=unix$DISPLAY \
#        -v `pwd`:/home/tkdiff \
# 	 weatherhub/tkdiff file1 file2
#

FROM debian:sid
LABEL maintainer "Xin Zhang <xin.zhang@longrunweather.com>"

RUN    apt-get update \
    && apt-get install -y git subversion tk tcl libx11-dev --no-install-recommends \
    && rm -rf /var/lib/apt/lists/*


COPY tkdiff /usr/bin/.

ENV HOME /home/tkdiff
RUN    useradd --create-home --home-dir $HOME tkdiff \
    && chown -R tkdiff:tkdiff $HOME

WORKDIR $HOME
USER tkdiff

ENTRYPOINT [ "tkdiff" ]
