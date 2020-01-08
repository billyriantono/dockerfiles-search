ARG BASE=confluentinc/cp-enterprise-kafka:5.0.1
ARG REGISTRY=vc11web
ARG WRAPPER=container-wrapper:v1

FROM $REGISTRY/$WRAPPER
 
###########################################

FROM $BASE

ARG BASE=confluentinc/cp-enterprise-kafka:5.0.1
ARG REGISTRY=vc11web
ARG WRAPPER=container-wrapper:v1
ARG IMAGE=kafka:base
ARG LABELNAMESPACE=io.vcweb

ENV entrypoint "/etc/confluent/docker/run"
ENV containerImage "$REGISTRY/$IMAGE"
ENV imageComponent "$IMAGE"
ENV imageBase "$BASE"
ENV imageWrapper "$REGISTRY/$WRAPPER"

COPY ./build/docker/* /etc/confluent/docker/
COPY ./build/kafka/* /etc/kafka/

USER root
COPY --from=0 /container-wrapper /container-wrapper/
COPY --from=0 /container-wrapper/docs/README.md /container-wrapper/docs/CONTAINER-WRAPPER.md
COPY ./Dockerfile /container-wrapper/setup/docker/Dockerfile
COPY ./README.md /container-wrapper/docs/README.md

COPY ./build/* /container-wrapper/setup/docker/

RUN chmod +x /container-wrapper/run-container.sh && \
    chmod +x /container-wrapper/input-to-level.sh && \
    chmod +x /container-wrapper/input-to-timestamp.sh && \
    chmod +x /container-wrapper/error-to-JSON.sh && \
    chmod +x /container-wrapper/text-to-JSON.sh && \
    chmod +x /container-wrapper/entrypoint.sh

ENTRYPOINT ["/container-wrapper/entrypoint.sh"]

LABEL $LABELNAMESPACE.schema-version="1.0"
LABEL $LABELNAMESPACE.name="Kafka"
LABEL $LABELNAMESPACE.description="This is a wrapped $BASE image."
LABEL $LABELNAMESPACE.docker.cmd.help="docker run $REGISTRY/$IMAGE --help"
LABEL $LABELNAMESPACE.image.name="$REGISTRY/$IMAGE"
LABEL $LABELNAMESPACE.image.base="$BASE"
LABEL $LABELNAMESPACE.image.wrapper="$WRAPPER"
LABEL $LABELNAMESPACE.image.type="component" 