FROM circleci/golang:1.8
MAINTAINER senbazuru

RUN curl https://glide.sh/get | sh
RUN curl "https://bootstrap.pypa.io/get-pip.py" -o "/tmp/get-pip.py"
RUN sudo python /tmp/get-pip.py
RUN sudo pip install awscli
