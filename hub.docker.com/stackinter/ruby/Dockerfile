FROM ruby:2.3
LABEL maintainer: "Sergey Shkarupa <s.shkarupa@gmail.com>"

RUN echo "deb http://www.deb-multimedia.org jessie main non-free" >> /etc/apt/sources.list && \
    echo "deb-src http://www.deb-multimedia.org jessie main non-free" >> /etc/apt/sources.list && \
    apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 5C808C2B65558117 && \
    apt-get update && apt-get install --force-yes -y deb-multimedia-keyring && \
    apt-get install -y --no-install-recommends ffmpeg ffmpegthumbnailer && \
    rm -rf /var/lib/apt/lists/* && \
    curl -sL https://deb.nodesource.com/setup_6.x | bash - && \
    apt-get install -y nodejs && \
    npm i mjml@3.2 -g

RUN mkdir -p /usr/src/app
WORKDIR /usr/src/app
