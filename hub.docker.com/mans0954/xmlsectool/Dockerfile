FROM ubuntu:bionic
RUN apt update && apt install -y default-jre wget unzip
RUN wget https://shibboleth.net/downloads/tools/xmlsectool/2.0.0/xmlsectool-2.0.0-bin.zip
# TODO check sha
RUN unzip xmlsectool-2.0.0-bin.zip

