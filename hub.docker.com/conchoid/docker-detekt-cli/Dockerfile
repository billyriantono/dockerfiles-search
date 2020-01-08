FROM openjdk:11.0.5-jdk-stretch AS detekt-cli

RUN VERSION="1.2.2" \
    && wget -q "https://github.com/arturbosch/detekt/archive/${VERSION}.tar.gz" \
    && tar xzf "${VERSION}.tar.gz" \
    && mv ./detekt-${VERSION} /detekt \
    && cd /detekt/detekt-cli \
    && (for _ in $(seq 20); do /detekt/gradlew build shadowJar && break || sleep 5; done) \
    && ls /detekt/detekt-cli/build/libs

FROM scratch

COPY --from=detekt-cli /detekt/detekt-cli/build/libs /detekt/detekt-cli
