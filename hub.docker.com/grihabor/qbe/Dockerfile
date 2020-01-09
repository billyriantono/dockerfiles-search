FROM alpine
MAINTAINER Nikita Malyshev <neketmal@gmail.com>

RUN apk update \
 && apk add make g++ git vim

ENV QBE_PATH /qbe
RUN git clone https://compilers.ispras.ru/git/qbe.git $QBE_PATH
WORKDIR $QBE_PATH

RUN make && make install DESTDIR=/usr

WORKDIR /project
