FROM ubuntu:14.04
MAINTAINER Raphael Bicker <raphael@bicker.ch>

# Install Cowsay
RUN apt-get update \
  && apt-get install -y cowsay

# Add Docker Cow
COPY docker.cow /usr/share/cowsay/cows/

# Set Docker Cow as Default
RUN rm -f /usr/share/cowsay/cows/default.cow \
  && ln -sv /usr/share/cowsay/cows/docker.cow /usr/share/cowsay/cows/default.cow

# Entrypoint & CMD
ENTRYPOINT [ "/usr/games/cowsay" ]
CMD [ "hello world" ]
