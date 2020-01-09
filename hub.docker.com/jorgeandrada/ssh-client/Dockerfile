FROM debian:stretch-slim

ARG BUILD_DATE
ARG VCS_REF
ARG VERSION
LABEL org.label-schema.build-date=$BUILD_DATE \
      org.label-schema.name="ssh-client" \
      org.label-schema.description="SSH client with ansi2html to get the output of the commands in html. (debian-slim)" \
      org.label-schema.url="http://andradaprieto.es" \
      org.label-schema.vcs-ref=$VCS_REF \
      org.label-schema.vcs-url="https://github.com/jandradap/ssh-client" \
      org.label-schema.vendor="Jorge Andrada Prieto" \
      org.label-schema.version=$VERSION \
      org.label-schema.schema-version="1.0" \
      maintainer="Jorge Andrada Prieto <jandradap@gmail.com>" \
      org.label-schema.docker.cmd="docker run -i jorgeandrada/ssh-client bash -c 'ls -lh | ansi2html' > output.html"

RUN apt-get update && apt-get install -y --no-install-recommends \
    openssh-client \
    python-pip \
  && rm -rf /var/lib/apt/lists/*

RUN pip install wheel \
  && pip install setuptools \
  && pip install ansi2html \
  && mkdir -p /root/.ssh \
  && chmod 0700 /root/.ssh \
  && echo "Host *\n\tStrictHostKeyChecking no\n\n" > /root/.ssh/config

CMD ["ssh"]
