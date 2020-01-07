FROM alpine:latest

ENV APP_ENV="dev"

ENV LANG       en_US.UTF-8
ENV LC_ALL     en_US.UTF-8


RUN mkdir -p /tpl
ADD tpl/* /tpl/
ADD ./run_tests.sh ./run_tests.sh

