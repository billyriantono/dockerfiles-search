FROM node:10.15.3

RUN apt-get update \
    && apt-get install -y \
    python3 \
    python3-pip \
    openssh-client \
    && pip3 install awscli

CMD ["python3"]
