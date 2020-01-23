FROM asciidoctor/docker-asciidoctor
LABEL MAINTAINER="Harry Lee"

RUN pip3 install --no-cache-dir \
	livereload

COPY livereload.sh /livereload.sh
RUN chmod +x /livereload.sh
