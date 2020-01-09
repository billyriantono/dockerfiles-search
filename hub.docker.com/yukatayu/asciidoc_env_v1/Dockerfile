FROM ubuntu:18.04

MAINTAINER Yukatayu
LABEL maintainer="Yukatayu <yukatayu@yukatayu.tech>"

RUN apt update -y && \
	apt upgrade -y && \
	apt install -y make git vim ruby && \
	gem install asciidoctor && \
	gem install --pre asciidoctor-pdf && \
	gem install asciidoctor-pdf-cjk && \
	gem install rouge && \
	apt install -y bison flex libffi-dev libxml2-dev libgdk-pixbuf2.0-dev libcairo2-dev libpango1.0-dev fonts-lyx cmake ruby-dev && \
	gem install asciidoctor-mathematical && \
	gem install asciidoctor-pdf-cjk-kai_gen_gothic && \
	asciidoctor-pdf-cjk-kai_gen_gothic-install && \
	echo "Successfully installed"


WORKDIR /documents
VOLUME /documents

ENTRYPOINT ["make"]

