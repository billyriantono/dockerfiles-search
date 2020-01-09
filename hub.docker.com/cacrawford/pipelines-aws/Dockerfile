FROM alpine:3.6

# Install packages needed to build
RUN apk add --update --no-cache \
    python \
    py-pip \
  && pip install --upgrade pip \
  && pip install -U awscli
