FROM infiniteproject/icecast

COPY icecast.xml /etc/icecast.xml

RUN apk update && \
    apk add curl && \
    apk update

#HEALTHCHECK --interval=1m --timeout=3s CMD curl --fail http://localhost:8000/ || exit 1