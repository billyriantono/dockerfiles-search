FROM alpine:3.9

# Image Metadata
LABEL \
  Name="JDK Base Image On Alpine" \
  Description="Oracle Java 8 Standard Edition Development Kit Base Image On Alpine" \
  Vendor="Issenn"\
  Version="0.1.0" \
  Maintainer="issenn <issenn@hellotalk.com>" \
  com.issenn.application.java.jdk.is-beta="" \
  com.issenn.application.java.jdk.is-production="" \
  com.issenn.application.java.jdk.version="" \
  com.issenn.application.image.build-date="2019-03-19" \
  com.issenn.application.image.release-date="2019-03-19"

# SHELL ["/bin/bash", "-c"]

# Container variables
ENV \
  TERM="xterm" \
  # LANG=C.UTF-8 \
  LANG="en_US.UTF-8" \
  # LANGUAGE=C.UTF-8 \
  LANGUAGE="en_US.UTF-8" \
  # LC_ALL=C.UTF-8 \
  LC_ALL="en_US.UTF-8" \
  TIMEZONE="Asia/Shanghai"

# RUN sed -i 's/dl-cdn.alpinelinux.org/mirrors.aliyun.com/' /etc/apk/repositories

# Set timezone and locales
RUN set -ex \
  && apk update \
  && apk upgrade \
  && apk add --no-cache \
          bash \
          tzdata \
          vim \
          tini \
          su-exec \
          gzip \
          tar \
          curl \
  && echo "${TIMEZONE}" > /etc/TZ \
  && ln -sf /usr/share/zoneinfo/${TIMEZONE} /etc/localtime \
  # Network fix
  && echo 'hosts: files mdns4_minimal [NOTFOUND=return] dns mdns4' >> /etc/nsswitch.conf \
  && sync

# Here we install GNU libc (aka glibc) and set en_US.UTF-8 locale as default.

RUN \
  ALPINE_GLIBC_BASE_URL="https://github.com/sgerrand/alpine-pkg-glibc/releases/download" && \
  ALPINE_GLIBC_PACKAGE_VERSION="2.29-r0" && \
  ALPINE_GLIBC_BASE_PACKAGE_FILENAME="glibc-$ALPINE_GLIBC_PACKAGE_VERSION.apk" && \
  ALPINE_GLIBC_BIN_PACKAGE_FILENAME="glibc-bin-$ALPINE_GLIBC_PACKAGE_VERSION.apk" && \
  ALPINE_GLIBC_I18N_PACKAGE_FILENAME="glibc-i18n-$ALPINE_GLIBC_PACKAGE_VERSION.apk" && \
  apk add --no-cache --virtual=.build-dependencies ca-certificates && \
  # echo \
  #   "-----BEGIN PUBLIC KEY-----\
  #   MIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEApZ2u1KJKUu/fW4A25y9m\
  #   y70AGEa/J3Wi5ibNVGNn1gT1r0VfgeWd0pUybS4UmcHdiNzxJPgoWQhV2SSW1JYu\
  #   tOqKZF5QSN6X937PTUpNBjUvLtTQ1ve1fp39uf/lEXPpFpOPL88LKnDBgbh7wkCp\
  #   m2KzLVGChf83MS0ShL6G9EQIAUxLm99VpgRjwqTQ/KfzGtpke1wqws4au0Ab4qPY\
  #   KXvMLSPLUp7cfulWvhmZSegr5AdhNw5KNizPqCJT8ZrGvgHypXyiFvvAH5YRtSsc\
  #   Zvo9GI2e2MaZyo9/lvb+LbLEJZKEQckqRj4P26gmASrZEPStwc+yqy1ShHLA0j6m\
  #   1QIDAQAB\
  #   -----END PUBLIC KEY-----" | sed 's/   */\n/g' > "/etc/apk/keys/sgerrand.rsa.pub" && \
  curl --fail --show-error --location --retry 3 \
    -o "/etc/apk/keys/sgerrand.rsa.pub" \
    "https://alpine-pkgs.sgerrand.com/sgerrand.rsa.pub" && \
  curl --fail --show-error --location --retry 3 \
    -O \
    "$ALPINE_GLIBC_BASE_URL/$ALPINE_GLIBC_PACKAGE_VERSION/$ALPINE_GLIBC_BASE_PACKAGE_FILENAME" \
    -O \
    "$ALPINE_GLIBC_BASE_URL/$ALPINE_GLIBC_PACKAGE_VERSION/$ALPINE_GLIBC_BIN_PACKAGE_FILENAME" \
    -O \
    "$ALPINE_GLIBC_BASE_URL/$ALPINE_GLIBC_PACKAGE_VERSION/$ALPINE_GLIBC_I18N_PACKAGE_FILENAME" && \
  apk add --no-cache \
    "$ALPINE_GLIBC_BASE_PACKAGE_FILENAME" \
    "$ALPINE_GLIBC_BIN_PACKAGE_FILENAME" \
    "$ALPINE_GLIBC_I18N_PACKAGE_FILENAME" && \
  \
  rm -f "/etc/apk/keys/sgerrand.rsa.pub" && \
  /usr/glibc-compat/bin/localedef --force --inputfile POSIX --charmap UTF-8 "$LANG" || true && \
  echo "export LANG=$LANG" > /etc/profile.d/locale.sh && \
  \
  apk del glibc-i18n && \
  \
  apk del .build-dependencies && \
  rm -f \
    "$ALPINE_GLIBC_BASE_PACKAGE_FILENAME" \
    "$ALPINE_GLIBC_BIN_PACKAGE_FILENAME" \
    "$ALPINE_GLIBC_I18N_PACKAGE_FILENAME" \
  && sync

# Install JDK 1.8.202

ENV \
  JAVA_VERSION_MAJOR=8 \
  JAVA_VERSION_MINOR=202 \
  JAVA_VERSION_BUILD=08 \
  JAVA_PACKAGE=jdk \
  JAVA_HASH=1961070e4c9b4e26a04e7f5a083f551e \
  JAVA_HOME="/usr/lib/jvm/default-jvm"

ENV \
  JAVA_8_HOME="/usr/lib/jvm/java-${JAVA_VERSION_MAJOR}-oracle" \
  PATH="${PATH}:${JAVA_HOME}/bin"
  # CLASSPATH=.:${JAVA_HOME}/lib/dt.jar:${JAVA_HOME}/lib/tools.jar

RUN \
  apk add --no-cache --virtual=build-dependencies ca-certificates unzip && \
  cd "/tmp" && \
  mkdir -p "${JAVA_8_HOME}" && \
  curl --fail --show-error --location --retry 3 -o - \
    --cookie "oraclelicense=accept-securebackup-cookie" \
    "http://download.oracle.com/otn-pub/java/jdk/${JAVA_VERSION_MAJOR}u${JAVA_VERSION_MINOR}-b${JAVA_VERSION_BUILD}/${JAVA_HASH}/${JAVA_PACKAGE}-${JAVA_VERSION_MAJOR}u${JAVA_VERSION_MINOR}-linux-x64.tar.gz" \
    | tar -xzf - -C "${JAVA_8_HOME}" --strip-components=1 && \
  ln -s "${JAVA_8_HOME}" "${JAVA_HOME}" && \
  # ln -s "$JAVA_HOME/bin/"* "/usr/bin/" && \
  rm -rf "${JAVA_HOME}/"*src.zip \
    "${JAVA_HOME}/lib/missioncontrol" \
    "${JAVA_HOME}/lib/visualvm" \
    "${JAVA_HOME}/lib/"*javafx* \
    "${JAVA_HOME}/jre/lib/plugin.jar" \
    "${JAVA_HOME}/jre/lib/ext/jfxrt.jar" \
    "${JAVA_HOME}/jre/bin/javaws" \
    "${JAVA_HOME}/jre/lib/javaws.jar" \
    "${JAVA_HOME}/jre/lib/desktop" \
    "${JAVA_HOME}/jre/plugin" \
    "${JAVA_HOME}/jre/lib/"deploy* \
    "${JAVA_HOME}/jre/lib/"*javafx* \
    "${JAVA_HOME}/jre/lib/"*jfx* \
    "${JAVA_HOME}/jre/lib/amd64/libdecora_sse.so" \
    "${JAVA_HOME}/jre/lib/amd64/"libprism_*.so \
    "${JAVA_HOME}/jre/lib/amd64/libfxplugins.so" \
    "${JAVA_HOME}/jre/lib/amd64/libglass.so" \
    "${JAVA_HOME}/jre/lib/amd64/libgstreamer-lite.so" \
    "${JAVA_HOME}/jre/lib/amd64/"libjavafx*.so \
    "${JAVA_HOME}/jre/lib/amd64/"libjfx*.so && \
  rm -rf "${JAVA_HOME}/jre/bin/jjs" \
    "${JAVA_HOME}/jre/bin/keytool" \
    "${JAVA_HOME}/jre/bin/orbd" \
    "${JAVA_HOME}/jre/bin/pack200" \
    "${JAVA_HOME}/jre/bin/policytool" \
    "${JAVA_HOME}/jre/bin/rmid" \
    "${JAVA_HOME}/jre/bin/rmiregistry" \
    "${JAVA_HOME}/jre/bin/servertool" \
    "${JAVA_HOME}/jre/bin/tnameserv" \
    "${JAVA_HOME}/jre/bin/unpack200" \
    "${JAVA_HOME}/jre/lib/ext/nashorn.jar" \
    "${JAVA_HOME}/jre/lib/jfr.jar" \
    "${JAVA_HOME}/jre/lib/jfr" \
    "${JAVA_HOME}/jre/lib/oblique-fonts" && \
  curl --fail --show-error --location --retry 3 -O \
    --cookie "oraclelicense=accept-securebackup-cookie" \
    "http://download.oracle.com/otn-pub/java/jce/${JAVA_VERSION_MAJOR}/jce_policy-${JAVA_VERSION_MAJOR}.zip" && \
  unzip -jo -d "${JAVA_HOME}/jre/lib/security" "jce_policy-${JAVA_VERSION_MAJOR}.zip" && \
  rm -f "${JAVA_HOME}/jre/lib/security/README.txt" && \
  apk del build-dependencies curl ca-certificates tar && \
  \
  echo 'public class Main { public static void main(String[] args) { System.out.println("Ф Java code is running fine!"); } }' > Main.java && \
  javac Main.java && \
  java Main && \
  rm -rf "/tmp/"* \
  && sync
