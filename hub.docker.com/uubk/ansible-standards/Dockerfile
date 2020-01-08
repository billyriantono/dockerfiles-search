# Make this repo "runnable"
FROM debian:stretch

ADD requirements.txt /data/
WORKDIR /data

RUN apt update && \
  apt install --no-install-recommends -y python-pip git ssh tar gzip ca-certificates python-setuptools python-wheel && \
  rm -Rf /var/lib/apt/lists/*

ADD . /data/
RUN pip install -r requirements.txt && \
  mkdir -p /root/.config/ansible-review/ && \
  mv /data/config.ini /root/.config/ansible-review/config.ini
