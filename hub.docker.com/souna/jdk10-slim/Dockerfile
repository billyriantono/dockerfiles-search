FROM souna/jdk10 AS builder

RUN /opt/jdk/bin/jlink \
    --module-path /opt/jdk/jmods \
    --verbose \
    --add-modules java.base,java.logging,java.xml,jdk.unsupported,java.sql,java.naming,java.desktop,java.management,java.security.jgss,java.instrument \
    --output /opt/jdk-minimal \
    --compress 2 \
    --no-header-files

# Second stage, add only custom jdk10 distribution
FROM debian:9-slim
WORKDIR /usr/src/app
COPY --from=builder /opt/jdk-minimal /opt/jdk-minimal
ENV JAVA_HOME=/opt/jdk-minimal
ENV PATH="$PATH:$JAVA_HOME/bin"
ENV APP_TIMEZONE=UTC
