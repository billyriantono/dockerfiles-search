#FROM ubuntu:latest
FROM debian:latest

LABEL maintainer "Dr. Maarten Becker <info@nuc-eng.com>"

ENV LANG=C.UTF-8 \
    LC_ALL=C.UTF-8 \
    TERM=xterm \
    PANDOCVER=2.7.3 \
    TLVER=2019

RUN PACKAGES="wget libswitch-perl" \
	&& apt-get update \
	&& apt-get upgrade -qq --no-install-recommends \
	&& apt-get install -qq $PACKAGES --no-install-recommends \
           gnuplot \
           make \
           git \
	   curl \
           ca-certificates \
           vim \
	&& apt-get install -qq python-pygments \
	&& wget -qO- http://mirror.ctan.org/systems/texlive/tlnet/install-tl-unx.tar.gz |\
		tar xz \
	&& cd install-tl-* \
	&& echo "selected_scheme scheme-full" > profile \
	&& echo "tlpdbopt_install_docfiles 0" >> profile \
	&& echo "tlpdbopt_install_srcfiles 0" >> profile \
	&& ./install-tl -profile profile \
	&& wget -q https://github.com/jgm/pandoc/releases/download/${PANDOCVER}/pandoc-${PANDOCVER}-1-amd64.deb \
	&& dpkg -i pandoc-${PANDOCVER}-1-amd64.deb \
# Cleanup
	&& rm -rf install-tl-* \
	&& apt-get remove --purge -qq $PACKAGES \
	&& apt-get autoremove --purge -qq \
	&& rm -rf /var/lib/apt/lists/* \
	&& rm pandoc-${PANDOCVER}-1-amd64.deb

ENV PATH /usr/local/texlive/${TLVER}/bin/x86_64-linux:${PATH}
USER root
WORKDIR /home/latex/work
