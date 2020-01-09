# Build image
FROM codereaper91/gcc:latest AS build

## Build environment
ENV LDFLAGS=-static
WORKDIR /usr/src/app

## Build files
COPY Makefile .
COPY src src/

## Build
RUN make

# Production image
FROM scratch

## Files
COPY --from=build /usr/src/app/athena /

## Environment
ENTRYPOINT [ "/athena" ]