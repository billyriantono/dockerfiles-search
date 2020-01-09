FROM ubuntu:xenial

RUN sed -i.bak -e "s%http://archive.ubuntu.com/ubuntu/%http://ftp.jaist.ac.jp/pub/Linux/ubuntu/%g" /etc/apt/sources.list && \
    apt-get update && \
    apt-get install -y --no-install-recommends \
        wget \
        texlive \
        texlive-latex-extra \
        texlive-lang-japanese \
        latexmk \
        inkscape \
        default-jre \
        graphviz && \
    rm -rf /var/lib/apt/lists/*

RUN kanji-config-updmap-sys auto

ENV PLANTUML_JAR=/opt/plantuml.jar
RUN wget http://jaist.dl.sourceforge.net/project/plantuml/plantuml.8048.jar -O ${PLANTUML_JAR}