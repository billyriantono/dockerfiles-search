FROM ubuntu:18.04
LABEL maintainer="kare@sifr.no <Kaare Andersen>"
LABEL description="A simple RESTful service wrapper for pandoc with latex"
ARG CTAN_MIRROR=http://ctan.uib.no/systems/texlive/tlnet
ARG PANDOC_VERSION=2.4
ARG PANDOC_DEB=pandoc-${PANDOC_VERSION}-1-amd64.deb
ENV DEBIAN_FRONTEND noninteractive
ENV PATH="/usr/local/texlive/2018/bin/x86_64-linux:${PATH}"
ENV PANDOC_VERSION 2.4
ENV HOME /work

RUN apt-get update -qy && apt-get install -qy build-essential wget libfontconfig1 python3-pip && \
			wget https://github.com/jgm/pandoc/releases/download/${PANDOC_VERSION}/${PANDOC_DEB} && \
			dpkg -i ${PANDOC_DEB}  && rm -f ${PANDOC_DEB} && \
			wget ${CTAN_MIRROR}/install-tl-unx.tar.gz \
			&& mkdir /install-tl-unx \
			&& tar -xvf install-tl-unx.tar.gz -C /install-tl-unx --strip-components=1 && \
			echo "selected_scheme scheme-basic" >> /install-tl-unx/texlive.profile && \
			/install-tl-unx/install-tl -profile /install-tl-unx/texlive.profile && \
			rm -r /install-tl-unx && \
			rm install-tl-unx.tar.gz && \
			tlmgr install latexmk lm ec  && \
			rm -f ${PANDOC_DEB} && apt-get -y --auto-remove purge build-essential  && \
			apt-get -y autoremove && apt-get -y clean

VOLUME ["/work"]
EXPOSE 10089
ADD ./api /api
WORKDIR /api
RUN pip3 install -r requirements.txt
CMD ["python3", "-u", "app.py"]
