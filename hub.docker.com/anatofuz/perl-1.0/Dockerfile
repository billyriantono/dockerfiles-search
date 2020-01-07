FROM ubuntu:latest as build-stage

RUN apt -y update && apt -y upgrade

RUN apt install -y build-essential gcc mercurial libgcc-7-dev gcc-multilib bison

RUN hg clone http://www.cr.ie.u-ryukyu.ac.jp/hg/Members/anatofuz/test_perl1_alpine/ Perl-1.0

WORKDIR Perl-1.0

RUN ["./Configure", "-d"]
RUN make 

FROM ubuntu:latest as exec-stage

COPY --from=build-stage /Perl-1.0/perl /usr/local/bin/

CMD ["/usr/local/bin/perl"]
