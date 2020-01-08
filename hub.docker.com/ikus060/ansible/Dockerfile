FROM buildpack-deps:stretch

RUN apt-get update && apt-get install -y --no-install-recommends \
                python python-dev python-pip openssh-client \
  && pip install pip setuptools --upgrade \
  && pip install ansible \
  && rm -rf /var/lib/apt/lists/*

# Needed. Otherwise break python3 encoding.
# see https://bugs.python.org/issue19846
ENV LANG=C.UTF-8
