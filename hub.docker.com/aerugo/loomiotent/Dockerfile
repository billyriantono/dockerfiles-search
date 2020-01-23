FROM jrottenberg/ffmpeg:4.1-ubuntu

ENV DEBIAN_FRONTEND noninteractive

RUN apt-get update && \
    apt-get install -y software-properties-common tzdata curl wget git vim build-essential autoconf automake libtool libssl-dev zlib1g-dev libmysqlclient-dev && \
    apt-add-repository -y ppa:brightbox/ruby-ng && \
    apt-get update && \
    apt-get install -y ruby2.6 ruby2.6-dev && \
    gem install bundler && \
    rm -rf /var/lib/apt/lists/*

ENTRYPOINT [""]
CMD ["irb"]
