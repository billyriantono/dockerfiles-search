FROM pandoc/latex:latest

RUN apk update
RUN apk add make
RUN apk add --no-cache texlive-full
RUN tlmgr update --self
RUN tlmgr install scheme-full

RUN apk add curl python3 python py-pip
# RUN apk add openjdk8-jre graphviz ttf-droid ttf-droid-nonlatin

RUN pip install pandocfilters
