FROM debian:jessie

LABEL maintainer="Alexis Pereda <alexis@pereda.fr>"
LABEL version="1.0"
LABEL description="Toolchain for CPOP"

RUN apt update \
	&& apt install --no-install-recommends --no-install-suggests -y \
		cmake g++ make libcgal-dev libgl1-mesa-dev qt4-default \
	&& rm -rf /var/lib/apt/lists/*

ENV USER_ID=1000
ENV CGAL_DIR=/usr/lib/CGAL

COPY ./entrypoint /usr/local/bin/

ENTRYPOINT ["/usr/local/bin/entrypoint"]
