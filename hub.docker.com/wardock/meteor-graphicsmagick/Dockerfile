FROM abernix/meteord:node-8.4.0-base
RUN echo "deb http://http.debian.net/debian jessie-backports main contrib non-free" >> /etc/apt/sources.list \
#RUN echo "deb http://ftp.debian.org/debian jessie-backports main" >> /etc/apt/sources.list \
&& apt-get -y update && apt-get install -y \
   graphicsmagick \
   graphicsmagick-imagemagick-compat \
   ffmpeg \
&& apt-get clean \
&& rm -rf /var/lib/apt/lists/*
