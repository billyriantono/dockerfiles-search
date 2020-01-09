# Creates a Docker container
# which is suitable for building and deploying 
# a hugo site to S3 via Gitlab CI.

FROM golang
MAINTAINER James Ethridge

RUN apt update \
&& apt-get -y install python-pip \
&& pip install awscli \
&& pip install Pygments \
&& go get -u -v github.com/gohugoio/hugo