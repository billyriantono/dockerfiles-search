#############################################
# GET/CACHE NPM DEPS
#############################################
FROM node:alpine as npm-dependencies
WORKDIR /app
# get npm modules (cache)
COPY ./react/package.json /app/react/
COPY ./react/package-lock.json /app/react/
RUN set -x \
    && cd /app/react \
    && npm install

#############################################
# BUILD REACT APP
#############################################
FROM node:alpine as frontend
# Copy app and build
COPY ./ /app
COPY --from=npm-dependencies /app/react/node_modules/ /app/react/node_modules/
RUN set -x \
    && cd /app/react/ \
    && npm run build \
    && cp /app/react/build/index.html /app/app/views/react.html \
    && rm -rf /app/public/js \
    && mkdir -p /app/public/js \
    && cp /app/react/build/static/js/* /app/public/js
# Import dependencies (bootstrap)
RUN set -x \
    && mkdir -p /app/public/dist/ \
	&& cp -r /app/react/node_modules/bootstrap/dist/ /app/public/dist/bootstrap \
	&& cp -r /app/react/node_modules/popper.js/dist/umd/ /app/public/dist/popper.js
# Cleanup react & node_modules
RUN rm -rf /app/react

#############################################
# BUILD GO APP
#############################################
FROM golang:1.12 as backend
WORKDIR /go/src/k8s-devops-console
COPY ./ /go/src/k8s-devops-console
RUN curl https://glide.sh/get | sh && glide install
RUN go get github.com/revel/cmd/revel
RUN go get -u github.com/golang/dep/cmd/dep
COPY --from=frontend /app/app/views/react.html /go/src/k8s-devops-console/app/views/react.html
COPY --from=frontend /app/public/js /go/src/k8s-devops-console/public/js
COPY --from=frontend /app/public/dist /go/src/k8s-devops-console/public/dist
RUN set -x \
    && CGO_ENABLED=0 GOOS=linux revel build k8s-devops-console /app prod \
    && rm -rf /app/src/k8s-devops-console/tests

#############################################
# FINAL IMAGE
#############################################
FROM gcr.io/distroless/static

ENV CONF_PATH=/app/src/k8s-devops-console/conf/app.conf
ENV APP_SECRET=please-change

COPY --from=backend /app/ /app/
USER 65534
EXPOSE 9000
CMD ["/app/k8s-devops-console", "-importPath", "k8s-devops-console", "-srcPath", "/app/src", "-runMode", "prod"]
