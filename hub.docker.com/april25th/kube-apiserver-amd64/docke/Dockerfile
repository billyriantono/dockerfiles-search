FROM ubuntu:latest
MAINTAINER Antoine Henning <henning.antoine@gmail.com>

# Get trusty-media apt-repository
RUN apt-get update && \
    apt-get install -y software-properties-common && \
    add-apt-repository -y ppa:mc3man/trusty-media && \
    apt-get update && apt-get upgrade -y

# Install ffmpeg
RUN apt-get install -y ffmpeg

# Clean-up
RUN apt-get autoclean -y && apt-get autoremove -y && apt-get clean -y && \
    rm -rf /var/lib/apt/lists/*

CMD ["ffmpeg"]