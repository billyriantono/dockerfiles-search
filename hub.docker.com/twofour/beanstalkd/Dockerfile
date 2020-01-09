FROM alpine:3.8

ARG BEANSTALKD_VERSION=1.10
EXPOSE 11300/tcp
ENV BEANSTALKD_BINLOG_INTERVAL=1000
COPY src /
RUN beanstalkd-setup
USER beanstalk
HEALTHCHECK CMD beanstalkd-healthcheck
ENTRYPOINT ["beanstalkd-entrypoint"]
CMD ["beanstalkd"]
