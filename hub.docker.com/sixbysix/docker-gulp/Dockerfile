FROM node:8.11-slim

ENV DEBIAN_FRONTEND noninteractive

RUN apt-get update && \
    apt-get install -y --no-install-recommends build-essential git ssh bzip2 python2.7  && \
    apt-get install -y --no-install-recommends curl && \
    apt-get autoremove -y && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/* && \
    rm -rf /var/cache/apt/* && \
    mkdir /workdir

RUN ln -s /usr/bin/python2.7 /usr/bin/python
RUN npm install gulp -g

VOLUME ["/workdir"]
WORKDIR /workdir

ENTRYPOINT ["/bin/bash", "-c"]
