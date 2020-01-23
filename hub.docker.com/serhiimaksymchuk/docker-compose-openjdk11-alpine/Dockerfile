# docker
FROM docker:latest

# compose
RUN apk add --no-cache py-pip
RUN pip install --upgrade pip
RUN pip install docker-compose
RUN apk add iptables

# java
ENV LANG C.UTF-8

ENV JAVA_HOME="/jdk-11"
ARG JDK_BUILD="28"
ENV JDK_ARCHIVE="openjdk-11+${JDK_BUILD}_linux-x64-musl_bin.tar.gz"


RUN echo "Downloading ${JDK_ARCHIVE}" \
    && wget https://download.java.net/java/early_access/alpine/${JDK_BUILD}/binaries/${JDK_ARCHIVE}

RUN echo "Downloading sha256 checksum" \
    && wget https://download.java.net/java/early_access/alpine/${JDK_BUILD}/binaries/${JDK_ARCHIVE}.sha256

RUN echo "Verify checksum" \
# exactly two spaces
    && echo "  ${JDK_ARCHIVE}" >> ${JDK_ARCHIVE}.sha256 \
    && sha256sum -c ${JDK_ARCHIVE}.sha256 \
    && echo "Checksum is correct"

RUN echo "Extract JDK" && tar -xzf ${JDK_ARCHIVE}

RUN rm ${JDK_ARCHIVE} ${JDK_ARCHIVE}.sha256
RUN rm ${JAVA_HOME}/lib/src.zip

ENV PATH=$PATH:${JAVA_HOME}/bin

ENV JAVA_VERSION 11-ea+${JDK_BUILD}
ENV JAVA_ALPINE_VERSION 11~${JDK_BUILD}-1

RUN echo $PATH && java --version && javac --version

ENTRYPOINT ["docker-entrypoint.sh"]
CMD ["sh"]

