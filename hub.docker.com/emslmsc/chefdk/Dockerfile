from chef/chefdk:1.0.3

ENV DEBIAN_FRONTEND=noninteractive

RUN apt-get update && \
    apt-get install -y git python2.7 python-pip python-virtualenv && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*
RUN virtualenv /opt/pre-commit && \
    . /opt/pre-commit/bin/activate && \
    pip install pre-commit
ENTRYPOINT ["/bin/bash", "--rcfile", "/opt/pre-commit/bin/activate"]
