FROM alpine:latest
ARG PROJ_DIR=/usr/src/carto_app
RUN mkdir -p ${PROJ_DIR}
COPY carto_app ${PROJ_DIR}
VOLUME ${PROJ_DIR}
CMD ["echo", "Data container for cartoview"]