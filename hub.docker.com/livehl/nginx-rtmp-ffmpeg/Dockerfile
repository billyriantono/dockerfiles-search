FROM tiangolo/nginx-rtmp
RUN echo "deb http://ftp.uk.debian.org/debian jessie-backports main" >> /etc/apt/sources.list && \
    apt-get update && \
    apt-get install -y ffmpeg && \
     apt-get install -y gettext && \
    rm -rf /var/lib/apt/lists/* &&\
    rm -rf /tmp/*
EXPOSE 80
EXPOSE 1935

