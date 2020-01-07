FROM binocarlos/nodejs
MAINTAINER 	Kai Davenport <kaiyadavenport@gmail.com>

RUN (mkdir /tmp/mon && cd /tmp/mon && curl -L# https://github.com/visionmedia/mon/archive/master.tar.gz | tar zx --strip 1 && make install)

ENTRYPOINT ["/usr/local/bin/mon", "/usr/local/bin/node"]
CMD [""]