FROM dannyzhong/aws-codebuild-docker-python3.6:latest

##########################################################################
#  Customize the build environment for our own stack
##########################################################################

RUN apt-get update

RUN apt-get install --yes less
RUN apt-get install --yes vim

RUN apt-get install --yes jq
# upgrade jq to 1.5. http://stackoverflow.com/questions/36462955/upgrading-jq-to-1-5-on-ubuntu
RUN wget https://github.com/stedolan/jq/releases/download/jq-1.5/jq-linux64 \
     && chmod +x jq-linux64 \
     && mv jq-linux64 $(which jq)

# Install node8. node7 can't be installed on ubuntu 17.10 (https://github.com/nodesource/distributions/issues/543)
RUN curl -sL https://deb.nodesource.com/setup_8.x | bash -
RUN apt-get install --yes nodejs
RUN pip3 install --upgrade pip setuptools
RUN pip3 install --upgrade --user awscli

