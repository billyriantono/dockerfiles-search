FROM circleci/openjdk:8-jdk-browsers
LABEL maintainer="Chris Montes"
LABEL description="Basic Docker image with OpenJDK and AWS CLI + cli53 for CircleCi workspaces"

RUN sudo mkdir -p /dir
ADD dependencies.sh /dir/
WORKDIR /dir
RUN sudo apt-get install apt-utils
RUN sudo chmod +x ./dependencies.sh
RUN ./dependencies.sh

CMD /bin/bash
