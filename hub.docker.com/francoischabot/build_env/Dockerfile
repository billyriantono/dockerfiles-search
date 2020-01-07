FROM        ubuntu:bionic
MAINTAINER  Francois Chabot <francois.chabot.dev@gmail.com>

# Default command on startup.
CMD bash

# Setup packages.
RUN apt-get update && apt-get -y install clang clang-format cmake git build-essential python3-pip
RUN pip3 install mkdocs
