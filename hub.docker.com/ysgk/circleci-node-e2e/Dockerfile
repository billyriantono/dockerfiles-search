FROM circleci/node:12-browsers

RUN sudo apt-get update
RUN sudo apt-get install -y \
# aws-cli
        python3-dev \
        python3-setuptools \
        python3-pip \
# japanese fonts
        fonts-ipafont-gothic \
        fonts-ipafont-mincho

RUN pip3 install awscli --upgrade --user

ENV PATH ~/.local/bin:$PATH

CMD ["node"]
