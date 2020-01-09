FROM ubuntu:bionic
MAINTAINER NHibiki https://github.com/NHibiki

COPY . /workdir

RUN /bin/bash /workdir/install

EXPOSE 2525
EXPOSE 80

ENTRYPOINT ["/bin/bash", "/usr/bin/run.sh"]