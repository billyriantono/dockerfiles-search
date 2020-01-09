FROM debian:sid-slim

RUN apt-get update && apt-get install --no-install-recommends -y \
		biber texlive-bibtex-extra\
		latexmk \
		texlive texlive-latex-extra texlive-fonts-extra texlive-science \
		curl \
		&& rm -rf /var/lib/apt/lists/*
