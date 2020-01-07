# For testing some Dockerfile commands

# Based on Ubuntu:14.04
FROM ubuntu:18.04

# Update system
RUN apt-get update -y

# Install github - code version control
RUN apt-get install -y git

# Install vim - editor
RUN apt-get install -y vim

# Install wget - downloader for Unix terminal
RUN apt-get install -y wget

# Install curl - downloader for Unix terminal
RUN apt-get install -y curl software-properties-common

# INSTALL NODEJS + NPM

RUN curl -sL https://deb.nodesource.com/setup_12.x -o nodesource_setup.sh
RUN bash nodesource_setup.sh
RUN apt-get install -y nodejs

# Set workspace - where to start working
# WORKDIR /workspace/

# ADD
# Usage: Add [source directory or URL] [destination directory]
# ADD README.md /mydata/README.md
# RUN echo "Copied a file"
# ADD tools/ /tools/
# RUN echo "Copied a folder"

# CMD
# Usage: CMD "application" "argument", "argument"
# CMD "echo" "I am CMD"

# ENTRYPOINT
# Usage: ENTRYPOINT application "argument","argument"
# ENTRYPOINT echo
# CMD "Hello docker"
# ENTRYPOINT echo

# ENV
# Usage: ENV key value
# ENV MYNAME Luong
# ENV MYEMAIL luongnv89@gmail.com

# RUN echo $MYNAME
# RUN echo $MYEMAIL

# EXPOSE
# Usage: EXPOSE [port]
# EXPOSE 8080

# USER
# Usage: USER [UID]
# RUN useradd luongnv89
# USER luongnv89

# VOLUME
# Usage: VOLUME ["/dir_1","dir_2",...]
#VOLUME ["~/projects","~/Downloads"]

# WORKDIR
# Usage: WORKDIR /path

# First message
RUN echo '*** Ubuntu: '`uname -a`'***"'
RUN echo '\n* git: '`git --version`
RUN echo '\n* vim: '`vi -version`
RUN echo '\n* nodejs: '`node -v`
RUN echo '\n* npm: '`npm -v`
RUN echo '\n*** END ***'
