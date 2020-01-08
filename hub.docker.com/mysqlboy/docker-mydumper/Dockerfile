FROM rikorose/gcc-cmake

RUN bzr branch lp:mydumper
WORKDIR mydumper
RUN cmake . && make

FROM debian:buster-slim

RUN apt-get -y -q update && apt-get install -y libglib2.0-0 libmariadb-dev-compat libmariadb-dev && apt-get clean && apt-get autoclean
COPY --from=0 /mydumper/my* /usr/bin/

CMD ["/bin/bash"]
