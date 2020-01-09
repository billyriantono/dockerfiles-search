FROM suzlab/python:latest

RUN apt-get update
RUN apt-get install -y groff
RUN apt-get clean

RUN pip install awscli
RUN ln -s /usr/local/bin/aws_bash_completer /etc/bash_completion.d/aws

WORKDIR /root

COPY .bashrc.patch ./
RUN patch .bashrc < .bashrc.patch
RUN rm .bashrc.patch

RUN git clone https://github.com/suz-lab/cloudformation.git
