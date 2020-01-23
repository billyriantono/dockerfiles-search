ARG VERSION=8
FROM openjdk:${VERSION}-jdk
LABEL maintainer="leoliang@gmail.com"
LABEL description="Kotlin development environment"

RUN apt-get update \
  && apt-get install zip --yes

SHELL ["/bin/bash", "-c"]

RUN curl -s "https://get.sdkman.io" | bash \
  && source "/root/.sdkman/bin/sdkman-init.sh" \
  && sdk install gradle \
  && sdk install maven \
  && sdk install kotlin

WORKDIR /project
