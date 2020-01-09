FROM debian:stretch-backports

RUN apt-get update && apt-get install -y \
		git \
		biber \
		latexmk \
		make \
		texlive-full \
	&& rm -rf /var/lib/apt/lists/*

