FROM unixlabs/openjdk:8
RUN apt-get update -y
RUN apt-get upgrade -y
RUN apt-get install wget curl nano unzip sudo apt-utils -y
RUN curl "https://s3.amazonaws.com/aws-cli/awscli-bundle.zip" -o "awscli-bundle.zip"
RUN unzip awscli-bundle.zip
RUN apt-get install python -y
RUN sudo ./awscli-bundle/install -i /usr/local/aws -b /usr/local/bin/aws
RUN apt-get install docker.io -y
