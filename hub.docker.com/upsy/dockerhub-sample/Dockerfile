FROM openjdk:11.0.5-jdk-stretch AS detekt-cli
#FROM openjdk:8u232-jdk-stretch AS detekt-cli

RUN VERSION="1.2.2" \
    && wget -q "https://github.com/arturbosch/detekt/archive/${VERSION}.tar.gz" \
    && tar xzf "${VERSION}.tar.gz" \
    && mv ./detekt-${VERSION} /detekt \
    && cd /detekt/detekt-cli && ../gradlew build shadowJar \
    && cd /detekt/detekt-sample-extensions && ../gradlew build \
    && ls /detekt/detekt-cli/build/libs \
    && ls /detekt/detekt-sample-extensions/build/libs \
    && mv /detekt /detekt_src \
    && mkdir /detekt \
    && cp -a /detekt_src/detekt-cli/build/libs /detekt/detekt-cli \
    && cp -a /detekt_src/detekt-sample-extensions/build/libs /detekt/detekt-sample-extensions \
    && rm -rf /detekt_src

FROM scratch

COPY --from=detekt-cli /detekt /detekt
#COPY --from=detekt-cli /detekt/detekt-cli/build/libs /detekt/detekt-cli
#COPY --from=detekt-cli /detekt/detekt-sample-extensions/build/libs /detekt/detekt-sample-extensions

