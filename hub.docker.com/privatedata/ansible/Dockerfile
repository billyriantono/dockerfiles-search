FROM debian:stretch
LABEL maintainer "Martin Schmidt <docker@private-data.de>"

RUN apt-get update && \
    apt-get install --no-install-recommends -y \
      python-wheel python-dev python-setuptools python-pip python-mysqldb && \
    rm -rf /var/lib/apt/lists/*

RUN pip install ansible

RUN mkdir /etc/ansible/ && \
    echo '[local]\nlocalhost\n' > /etc/ansible/hosts

CMD bash
