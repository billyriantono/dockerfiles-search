FROM sameersbn/gitlab-ci-multi-runner:1.1.4-5

RUN cd / && \
    wget https://get.docker.com/builds/Linux/x86_64/docker-1.12.3.tgz && \
    tar zxf docker-1.12.3.tgz && \
    rm docker-1.12.3.tgz
RUN sudo apt-get update && \
    sudo apt-get install -y python-pip && \
    sudo pip install awscli --ignore-installed six
