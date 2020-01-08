FROM circleci/python:latest

RUN curl https://sh.rustup.rs -sSf | sh -s -- -y
ENV PATH /home/circleci/.cargo/bin:$PATH
RUN rustup install 1.15.1
