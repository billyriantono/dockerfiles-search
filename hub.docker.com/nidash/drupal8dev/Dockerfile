FROM drupal:8.5.5

ADD ./scripts /build-scripts

RUN ["chmod", "+x", "-R", "/build-scripts"]

RUN /build-scripts/php.sh && \
    /build-scripts/install.sh && \
    /build-scripts/env.sh && \
    rm -rf /build-scripts