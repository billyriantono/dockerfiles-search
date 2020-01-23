FROM circleci/ruby:2.6.1-stretch

ENV PATH="/home/circleci/.local/bin:${PATH}"

WORKDIR /home/circleci

RUN sudo apt-get install python-dev && \
    curl -O https://bootstrap.pypa.io/get-pip.py && \
    python get-pip.py --user && \
    pip install awscli --upgrade --user
