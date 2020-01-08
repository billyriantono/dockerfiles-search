FROM python:3.7-alpine
ENV BUILDPIPE_VERSION=0.3.1
WORKDIR /data
RUN apk add --no-cache git
RUN pip install --no-cache-dir buildpipe==${BUILDPIPE_VERSION}
ENTRYPOINT ["buildpipe"]
