FROM circleci/node:8-browsers
MAINTAINER Minn Soe <contributions@minn.io>


USER root
RUN apt-get update && apt-get install -y \
    groff \
    less \
    python-dev \
    python-pip \
&& rm -rf /var/lib/apt/lists/*


USER circleci
RUN pip install --upgrade --user awscli
ENV PATH ~/.local/bin:$PATH
