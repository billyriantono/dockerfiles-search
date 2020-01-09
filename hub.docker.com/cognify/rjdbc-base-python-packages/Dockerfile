# base image
FROM cognify/rjdbc-base-r-packages-2

MAINTAINER Norbert Walchhofer <nw@cognify.ai>

RUN pip3 install --no-cache-dir pystan
RUN pip3 install fbprophet --no-cache-dir --no-binary :all:

CMD ["/usr/bin/R"]