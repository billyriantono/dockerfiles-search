# ------------------------------------------------------------------------------
# \\\\\\\\\\\\\\\\\\\\\\\\\\\ \m/ dAnarchy.site \m/ ////////////////////////////
# ------------------------------------------------------------------------------
#
# - build the image:
# > docker build -t danarchy/alpine:latest .
#
# - run a container named as image
# > docker run -t -i -h image --name image --rm -e ENV_USER_UID=`id -u` danarchy/alpine:latest /bin/bash -l
#
# \\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\////////////////////////////////////////

FROM alpine:3.4

MAINTAINER danarchy.site <dnrk@protonmail.com>

RUN apk update
RUN apk upgrade
RUN apk add --no-cache alpine-sdk bash tmux python3 wget curl git vim htop \
                       youtube-dl
RUN apk add --no-cache ffmpeg
RUN wget https://yt-dl.org/downloads/latest/youtube-dl \
        -O /usr/local/bin/youtube-dl && \
        chmod a+rx /usr/local/bin/youtube-dl
RUN rm -rf /tmp/* && rm -rf /var/cache/apk/*

COPY dotfiles/ /root/
RUN ln -s /root/.bashrc /root/.profile

RUN echo "root:toor" | chpasswd

COPY entrypoint /usr/local/bin/entrypoint
RUN chmod +x /usr/local/bin/entrypoint
ENTRYPOINT ["/usr/local/bin/entrypoint"]
