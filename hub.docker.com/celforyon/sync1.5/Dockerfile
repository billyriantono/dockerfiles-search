FROM debian:stretch

LABEL maintainer="Alexis Pereda <alexis@pereda.fr>"
LABEL version="1.0"
LABEL description="Firefox Sync 1.5"

RUN apt update \
	&& apt install --no-install-recommends --no-install-suggests -y \
		gcc g++ make python-dev python-pip \
	&& rm -rf /var/lib/apt/lists/*

RUN pip install virtualenv

COPY syncserver /opt/syncserver
COPY syncserver.ini /opt/syncserver/syncserver.ini
WORKDIR /opt/syncserver

RUN make build

COPY bin/* /usr/local/bin

ENV PORT                5000
ENV WORKERS             1
ENV TIMEOUT             30
ENV PUBLIC_URL          http://localhost:5000
ENV SQLURI              sqlite:////tmp/syncserver.db
ENV SECRET              e57e59307bfaf654463158537bc42bb658ac5fbd
ENV ALLOW_NEW_USERS     false
ENV FORCE_WSGI_ENVIRON  false

EXPOSE 5000

CMD [ "/usr/local/bin/start" ]
