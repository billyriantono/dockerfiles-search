FROM openjdk:11-jdk

LABEL maintainer="frm.adiputra@gmail.com"

RUN cd /usr/local \
    && git clone --depth=1 https://github.com/asciidoctor/asciidoctor-fopub.git

RUN cd /usr/local/asciidoctor-fopub \
    && ./gradlew -p "/usr/local/asciidoctor-fopub" -q -u installDist

COPY ./fopub /usr/local/bin/

RUN chmod +x /usr/local/bin/fopub

WORKDIR /documents
VOLUME /documents

CMD ["/bin/bash"]
