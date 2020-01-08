ARG REGISTRY=vc11web
ARG BASE=container-wrapper:v1

FROM $REGISTRY/$BASE

ARG REGISTRY=vc11web
ARG BASE=container-wrapper:v1
ARG IMAGE=infometis-swarm:v1
ARG LABELNAMESPACE=io.vcweb

ENV containerImage "$REGISTRY/$IMAGE"
ENV imageComponent "$IMAGE"
ENV imageBase "$BASE"
ENV imageWrapper "$REGISTRY/$BASE"

RUN mv /container-wrapper/docs/README.md /container-wrapper/docs/CONTAINER-WRAPPER.md

COPY ./docs/ /container-wrapper/docs/
COPY ./README.md /container-wrapper/docs/README.md
COPY ./Dockerfile /container-wrapper/setup/docker/Dockerfile

COPY ./actions/ /container-wrapper/setup/actions/
RUN chmod -R +x /container-wrapper/setup/actions/*.sh
COPY ./build/ /container-wrapper/setup/build/
COPY ./docker-stack/ /container-wrapper/setup/docker-stack/
COPY ./docker-stack-standalone/ /container-wrapper/setup/docker-stack-standalone/
COPY ./manual-configuration/ /container-wrapper/setup/manual-configuration/
       
LABEL $LABELNAMESPACE.schema-version="1.0"
LABEL $LABELNAMESPACE.name="Infometis Swarm"
LABEL $LABELNAMESPACE.description="This image contains the $REGISTRY/$IMAGE self-monitoring stream processing swarm stack."
LABEL $LABELNAMESPACE.image.name="$REGISTRY/$IMAGE"
LABEL $LABELNAMESPACE.image.base="$REGISTRY/$BASE"
LABEL $LABELNAMESPACE.image.type="solution"
