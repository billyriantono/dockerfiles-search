FROM node:alpine AS frontend-builder
WORKDIR /go/src/coolerfall.com/colina
ADD ./frontend /go/src/coolerfall.com/colina/frontend
RUN apk --no-cache add git && \
    cd /go/src/coolerfall.com/colina/frontend/embed && \
    yarn install && yarn build && \
    cd /go/src/coolerfall.com/colina/frontend/admin && \
    yarn install && yarn build

# A image to build golang application.
FROM anbillon/go-builder AS backend-builder
WORKDIR /go/src/coolerfall.com/colina
# Copy the local package files to the container's workspace.
ADD ./backend /go/src/coolerfall.com/colina/backend
RUN apk --no-cache add ca-certificates && \
    cd /go/src/coolerfall.com/colina && \
    mkdir -p bin/dist
COPY --from=frontend-builder /go/src/coolerfall.com/colina/frontend/embed/dist \
    /go/src/coolerfall.com/colina/bin/dist/embed
COPY --from=frontend-builder /go/src/coolerfall.com/colina/frontend/admin/dist \
    /go/src/coolerfall.com/colina/bin/dist/admin
ARG VERSION
ARG GITCOMMIT
ARG BUILDTIME
RUN cd /go/src/coolerfall.com/colina/backend && \
    dep ensure -v && \
    CGO_ENABLED=0 GOOS=linux packr build -a -tags netgo -ldflags \
    "-w \
     -X 'coolerfall.com/colina/backend/misc.Version=$VERSION' \
     -X 'coolerfall.com/colina/backend/misc.GitCommit=$GITCOMMIT' \
     -X 'coolerfall.com/colina/backend/misc.BuildTime=$BUILDTIME'" -o colina && \
    mv colina ../bin/

# Make golang application image.
FROM alpine:3.8
MAINTAINER Vincent Cheung <coolingfall@gmail.com>
COPY --from=backend-builder /go/src/coolerfall.com/colina/bin/colina /usr/local/bin/
COPY --from=backend-builder /etc/ssl/certs/ca-certificates.crt /etc/ssl/certs/
# Run the container by default when the container starts.
COPY docker-entrypoint.sh /usr/local/bin/
RUN chmod +x /usr/local/bin/docker-entrypoint.sh && \
    apk add --no-cache postgresql-client
ENTRYPOINT ["docker-entrypoint.sh"]
CMD ["colina", "serve"]
EXPOSE 3000
