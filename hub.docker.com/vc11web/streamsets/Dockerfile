ARG BASE=streamsets/datacollector:3.5.2
ARG REGISTRY=vc11web
ARG WRAPPER=container-wrapper:v1

FROM $REGISTRY/$WRAPPER
 
###########################################

FROM $BASE

ARG BASE=streamsets/datacollector:3.5.2
ARG REGISTRY=vc11web
ARG WRAPPER=container-wrapper:v1
ARG IMAGE=streamsets:base
ARG LABELNAMESPACE=io.vcweb

ENV entrypoint "/docker-entrypoint.sh"
ENV containerImage "$REGISTRY/$IMAGE"
ENV imageComponent "$IMAGE"
ENV imageBase "$BASE"
ENV imageWrapper "$REGISTRY/$WRAPPER"

USER root

COPY ./build/install-libraries.sh /container-wrapper/config/install-libraries.sh
COPY ./build/sdc.properties /etc/sdc/sdc.properties
RUN chmod +x /container-wrapper/config/install-libraries.sh && \
    bash /container-wrapper/config/install-libraries.sh && \
    apk update && \
    apk add coreutils

COPY --from=0 /container-wrapper /container-wrapper/
COPY --from=0 /container-wrapper/docs/README.md /container-wrapper/docs/CONTAINER-WRAPPER.md
COPY ./Dockerfile /container-wrapper/setup/docker/Dockerfile
COPY ./README.md /container-wrapper/docs/README.md

COPY ./build/* /container-wrapper/setup/docker/build/

RUN chmod 777 /container-wrapper && \
    chown -R sdc /container-wrapper/ && \
    mkdir /output && \
    chmod 777 /output && \
    chown -R sdc /output

#USER sdc

ENTRYPOINT ["/container-wrapper/entrypoint.sh"]
       
LABEL $LABELNAMESPACE.schema-version="1.0"
LABEL $LABELNAMESPACE.name="Streamsets"
LABEL $LABELNAMESPACE.description="This is a wrapped $BASE image."
LABEL $LABELNAMESPACE.docker.cmd.help="docker run $REGISTRY/$IMAGE --help"
LABEL $LABELNAMESPACE.image.name="$REGISTRY/$IMAGE"
LABEL $LABELNAMESPACE.image.base="$BASE"
LABEL $LABELNAMESPACE.image.wrapper="$WRAPPER"
LABEL $LABELNAMESPACE.image.type="component"