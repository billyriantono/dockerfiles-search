FROM albertalvarezbruned/lamp:php

# Set environment variables.
ENV HOME /root

# Define working directory.
WORKDIR /root

# Define default command.
CMD ["bash"]

ENV DEBIAN_FRONTEND noninteractive

# Install Nginx.
RUN apt-get update
RUN  apt-get install -y software-properties-common
RUN  add-apt-repository -y ppa:nginx/stable
# RUN  apt-get update
RUN  apt-get install -y nginx
RUN  rm -rf /var/lib/apt/lists/*
RUN  chown -R www-data:www-data /var/lib/nginx

# Define working directory.
WORKDIR /etc/nginx
RUN apt-get clean

# Copy all config files
#COPY ./config/default.conf /etc/nginx/conf.d/default.conf
COPY ./nginx.conf /etc/nginx/nginx.conf

# Define default command.
CMD nginx
