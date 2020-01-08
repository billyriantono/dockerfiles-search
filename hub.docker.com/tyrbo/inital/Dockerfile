FROM ubuntu:14.04.4
MAINTAINER Jonmichael Chambers <jon@tyrbo.net>

RUN mkdir -p /home/app
RUN groupadd -r app -g 433 && \
  useradd -u 431 -r -g app -d /home/app -s /sbin/nologin -c "Docker image user" app && \
  chown -R app:app /home/app

USER app

CMD ["/bin/bash"]
