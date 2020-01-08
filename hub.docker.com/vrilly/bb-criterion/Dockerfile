FROM atlassian/default-image:2

MAINTAINER tom@moulard.org
ENV DEBIAN_FRONTEND=noninteractive

RUN apt update
RUN apt install -y cmake man autoconf

# Criterion
RUN wget https://github.com/Snaipe/Criterion/releases/download/v2.3.3/criterion-v2.3.3-linux-x86_64.tar.bz2
RUN tar xvf criterion-v2.3.3-linux-x86_64.tar.bz2
RUN cp -r criterion-v2.3.3/lib/* /usr/lib/
RUN cp -r criterion-v2.3.3/include/* /usr/include/

RUN rm criterion-v2.3.3-linux-x86_64.tar.bz2
