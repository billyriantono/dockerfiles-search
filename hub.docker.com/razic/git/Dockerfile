FROM ubuntu

ENV HOME /root

RUN apt-get update && \
    apt-get install -y git

ADD .gitconfig ${HOME}/.gitconfig

ENTRYPOINT ["git"]
