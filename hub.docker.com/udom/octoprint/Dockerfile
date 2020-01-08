FROM pypy:2

MAINTAINER Udo Meijer <umeijer@gmail.com>

ENV OCTOPRINT_VERSION=1.3.10

RUN curl -s -L https://github.com/foosel/OctoPrint/archive/$OCTOPRINT_VERSION.tar.gz | tar xzf - \
 && cd OctoPrint-$OCTOPRINT_VERSION \
 && pip install --no-cache-dir . \
 && cd .. && rm -rf OctoPrint-$OCTOPRINT_VERSION

VOLUME /data

EXPOSE 5000

CMD ["octoprint", "serve", "--iknowwhatimdoing", "--basedir", "/data"]
