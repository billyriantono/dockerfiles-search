FROM ubuntu:latest AS build

RUN apt-get update && apt-get install -y build-essential
COPY nist/ /src
RUN mkdir /opt/nist
WORKDIR /src
RUN ./setup.sh /opt/nist --STDLIBS --without-X11 --64
RUN make config
RUN make it
RUN make install LIBNBIS=no

FROM ubuntu:latest
COPY --from=build /opt/nist /opt/nist
