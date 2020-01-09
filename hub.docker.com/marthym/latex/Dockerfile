FROM debian:testing-slim
LABEL maintainer="marthym@github.com"

# Update dependency
RUN export DEBIAN_FRONTEND=noninteractive && \
	apt -y update && \ 
	apt --no-install-recommends -y install \ 
		openssh-client \ 
        git \
		texlive-base \ 
		texlive-xetex \ 
		texlive-latex-recommended \
		texlive-latex-extra \ 
		texlive-extra-utils \ 
		texlive-fonts-recommended \ 
		texlive-font-utils \ 
		texlive-lang-french \ 
		texlive-pictures \ 
		texlive-bibtex-extra \ 
		lmodern biber latexmk ghostscript && \
	apt clean && \
	apt autoclean && \
	rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*
