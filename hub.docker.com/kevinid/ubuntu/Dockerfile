FROM kevinid/ubuntu:tensorflow-latest

LABEL maintainer="kevinid4g@gmail.com"

RUN apt-get update && \
    apt-get install -y --no-install-recommends python-rdkit

RUN pip2.7 --no-cache-dir install networkx molvs

# entrypoint is inherited from parent