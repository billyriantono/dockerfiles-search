FROM alpine:3.10 as build

ENV JAVA_SOURCE https://download.java.net/java/early_access/alpine/15/binaries/openjdk-14-ea+15_linux-x64-musl_bin.tar.gz
#ENV JAVA_SOURCE ./openjdk-14-ea+15_linux-x64-musl_bin.tar.gz
ENV JAVA_HOME /opt/jdk
ENV PATH $JAVA_HOME/bin:$PATH

ADD $JAVA_SOURCE /opt/tarball.tgz

RUN mkdir -p $JAVA_HOME \
    && tar -xzf /opt/tarball.tgz -C $JAVA_HOME --strip-components=1 \
    && jlink --compress=2 \
        --module-path /opt/jdk/jmods \
        # --add-modules java.base,java.sql,java.logging,java.naming,java.instrument,java.management,java.xml,jdk.sctp,jdk.unsupported \
        --add-modules jdk.jfr,jdk.management.agent,java.base,java.logging,java.xml,jdk.unsupported,java.sql,java.sql.rowset,java.naming,java.desktop,java.management,java.security.jgss,java.instrument \
        --no-header-files \
        --no-man-pages \
        --output /jlinked

FROM alpine:3.10
COPY --from=build /jlinked /opt/jdk/
ENV PATH /opt/jdk/bin:$PATH
CMD ["java", "--version"]
