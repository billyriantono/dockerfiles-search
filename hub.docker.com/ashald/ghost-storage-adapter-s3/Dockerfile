FROM node:8-alpine as builder
ENV BUILDDIR=/build
COPY package.json $BUILDDIR/
COPY src $BUILDDIR/src/
WORKDIR $BUILDDIR
RUN npm install && npm run build

# just so that container can be started, otherwise scratch would've worked
FROM busybox
ENV BUILDDIR=/build
ENV WORKDIR=/var/lib/ghost/content/adapters/storage/s3
COPY --from=builder /build $WORKDIR/
VOLUME ["$WORKDIR"]
CMD ["true"]
