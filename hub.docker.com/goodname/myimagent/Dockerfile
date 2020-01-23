FROM alpine:3.8 as builder

MAINTAINER Igor Popov <gonadarian@gmail.com>

RUN apk add --no-cache curl

WORKDIR /root/

ENV JAVA_VERSION_EA=5
ENV JAVA_VERSION=ea+${JAVA_VERSION_EA}_linux-x64-musl

RUN curl -fsSL https://download.java.net/java/early_access/alpine/${JAVA_VERSION_EA}/binaries/openjdk-12-${JAVA_VERSION}_bin.tar.gz | tar xzf - -C /usr/share && \
    ln -s /usr/share/jdk-12/bin/java /usr/bin/java

RUN cd /usr/share/jdk-12/bin && \
    ./jlink \
    --no-header-files \
    --no-man-pages \
    --output ~/jre \
    --module-path ../jmods \
    --add-modules java.base,java.compiler,java.datatransfer,java.instrument,java.logging,java.management,java.management.rmi,java.naming,java.net.http,java.prefs,java.rmi,java.scripting,java.security.jgss,java.security.sasl,java.smartcardio,java.sql,java.sql.rowset,java.transaction.xa,java.xml,java.xml.crypto

FROM alpine:3.8

COPY --from=builder /root/jre /usr/share/jre-12

RUN ln -s /usr/share/jre-12/bin/java /usr/bin/java

CMD [ "java", "--version" ]
