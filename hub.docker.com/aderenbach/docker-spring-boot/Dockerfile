# see https://github.com/jeanblanchard/docker-busybox-java
FROM jeanblanchard/busybox-java:8

MAINTAINER Alexander Derenbach <dea@zuehlke.com>

RUN opkg-install bash

ENV SPRING_BOOT_VERSION_MAJOR 1
ENV SPRING_BOOT_VERSION_MINOR 2
ENV SPRING_BOOT_VERSION_BUILD 3

ENV SPRING_DIR_NAME spring-${SPRING_BOOT_VERSION_MAJOR}.${SPRING_BOOT_VERSION_MINOR}.${SPRING_BOOT_VERSION_BUILD}.RELEASE

RUN curl -jksSL http://repo.spring.io/release/org/springframework/boot/spring-boot-cli/${SPRING_BOOT_VERSION_MAJOR}.${SPRING_BOOT_VERSION_MINOR}.${SPRING_BOOT_VERSION_BUILD}.RELEASE/spring-boot-cli-${SPRING_BOOT_VERSION_MAJOR}.${SPRING_BOOT_VERSION_MINOR}.${SPRING_BOOT_VERSION_BUILD}.RELEASE-bin.tar.gz \
      | gunzip -c - | tar -xf - -C /opt/ &&\
      ln -s /opt/${SPRING_DIR_NAME} /opt/springboot 

ENV PATH ${PATH}:/opt/springboot/bind
