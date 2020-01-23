FROM ubuntu:latest
MAINTAINER "Alex Coco" <hello@alexcoco.com>

# Get add-apt-repository and curl
RUN apt-get update -y && \
    apt-get install -y software-properties-common apt-transport-https curl

# Get heroku
RUN add-apt-repository "deb https://cli-assets.heroku.com/branches/stable/apt ./" && \
    curl -L https://cli-assets.heroku.com/apt/release.key | apt-key add - && \
    apt-get update -y && \
    apt-get install -y heroku

CMD ["/bin/bash"]
