FROM ubuntu:trusty

RUN apt-get update && DEBIAN_FRONTEND=noninteractive apt-get install -yq python-pip; apt-get clean && rm -rf /var/lib/apt/lists/* /var/tmp/* /tmp/*
RUN pip install dispy

CMD /usr/local/bin/dispynode.py -d
