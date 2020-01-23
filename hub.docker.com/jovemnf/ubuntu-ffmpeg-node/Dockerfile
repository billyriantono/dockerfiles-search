FROM ubuntu

RUN apt-get update
RUN apt-get install -y ffmpeg \
    curl
RUN curl -sL https://deb.nodesource.com/setup_9.x
RUN apt-get update && apt-get install -y nodejs \
    npm \
    build-essential \
    git
