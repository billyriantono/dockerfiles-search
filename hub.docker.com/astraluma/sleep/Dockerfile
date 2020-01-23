FROM gcc AS build
WORKDIR /tmp

COPY sleep.c .
RUN gcc sleep.c -static -o sleep

FROM scratch
MAINTAINER Jamie Bliss <jamie@ivyleav.es>

COPY --from=build /tmp/sleep /
CMD ["/sleep"]
