# Dockerfile
FROM ubuntu:16.04
MAINTAINER Uwe Grawert
LABEL description="Latex environment with common packages"
ENV DEBIAN_FRONTEND noninteractive
RUN apt-get --yes update && \
    apt-get --yes dist-upgrade
RUN apt-get --yes --no-install-recommends --no-install-suggests install \
        texlive \
        texlive-binaries \
        texlive-xetex \
        texlive-latex-base \
        texlive-latex-extra \
        texlive-generic-extra \
        texlive-fonts-extra \
        lmodern
RUN apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*
WORKDIR /data
VOLUME ["/data"]
ENTRYPOINT ["xelatex", "-shell-escape", "-file-line-error", "-interaction=nonstopmode"]
CMD ["index.tex"]
