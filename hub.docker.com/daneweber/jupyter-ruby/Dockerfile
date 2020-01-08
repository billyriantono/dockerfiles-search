FROM jupyter/minimal-notebook

USER root

# Add ecell4 dependencies
RUN apt-get update && apt-get install -y \
  libtool \
  libffi-dev \
  ruby \
  ruby-dev \
  make \
  libzmq3-dev \
  libczmq-dev

RUN gem update --no-document --system && gem install --no-document cztop iruby

USER jovyan

RUN iruby register --force
