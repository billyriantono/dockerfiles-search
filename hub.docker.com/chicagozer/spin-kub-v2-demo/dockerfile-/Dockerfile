FROM docker

RUN apk update && \
  apk add --no-cache gcc musl-dev rust cargo python3 curl && \
  curl -O https://bootstrap.pypa.io/get-pip.py && \
  python3 get-pip.py && \
  pip3 install awscli && \
  cargo install toast && \
  mv /root/.cargo/bin/toast /bin/toast
