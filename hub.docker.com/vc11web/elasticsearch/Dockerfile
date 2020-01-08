ARG BASE=docker.elastic.co/elasticsearch/elasticsearch:6.4.3
ARG REGISTRY=vc11web
ARG WRAPPER=container-wrapper:v1

FROM $REGISTRY/$WRAPPER
 
###########################################

FROM $BASE

ARG BASE=docker.elastic.co/elasticsearch/elasticsearch:6.4.3
ARG REGISTRY=vc11web
ARG WRAPPER=container-wrapper:v1
ARG IMAGE=elasticsearch:base
ARG LABELNAMESPACE=io.vcweb

USER root
COPY ./build/* /usr/share/elasticsearch/config/
RUN rm -rf /usr/share/elasticsearch/plugins/x-pack

ENV entrypoint "/usr/local/bin/docker-entrypoint.sh"
ENV containerImage "$REGISTRY/$IMAGE"
ENV imageComponent "$IMAGE"
ENV imageBase "$BASE"
ENV imageWrapper "$REGISTRY/$WRAPPER"

COPY --from=0 /container-wrapper /container-wrapper/
COPY --from=0 /container-wrapper/docs/README.md /container-wrapper/docs/CONTAINER-WRAPPER.md
COPY ./Dockerfile /container-wrapper/setup/docker/Dockerfile
COPY ./README.md /container-wrapper/docs/README.md
COPY ./build /container-wrapper/setup/build/

RUN chmod +x /container-wrapper/run-container.sh && \
    chmod +x /container-wrapper/input-to-level.sh && \
    chmod +x /container-wrapper/input-to-timestamp.sh && \
    chmod +x /container-wrapper/error-to-JSON.sh && \
    chmod +x /container-wrapper/text-to-JSON.sh && \
    chmod +x /container-wrapper/entrypoint.sh

ENTRYPOINT ["/container-wrapper/entrypoint.sh"]

LABEL $LABELNAMESPACE.schema-version="1.0"
LABEL $LABELNAMESPACE.name="ElasticSearch"
LABEL $LABELNAMESPACE.description="This is a wrapped $BASE image."
LABEL $LABELNAMESPACE.docker.cmd.help="docker run $REGISTRY/$IMAGE --help"
LABEL $LABELNAMESPACE.image.name="$REGISTRY/$IMAGE"
LABEL $LABELNAMESPACE.image.base="$BASE"
LABEL $LABELNAMESPACE.image.wrapper="$WRAPPER"
LABEL $LABELNAMESPACE.image.type="component"
