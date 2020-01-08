FROM alpine:3.8

RUN apk add --no-cache perl-libwww perl-datetime
RUN wget https://aws-cloudwatch.s3.amazonaws.com/downloads/CloudWatchMonitoringScripts-1.2.2.zip && \
    unzip CloudWatchMonitoringScripts-1.2.2.zip && \
    rm CloudWatchMonitoringScripts-1.2.2.zip

WORKDIR /aws-scripts-mon
RUN sed -i 's/-k -l -P/-kP/g' mon-put-instance-data.pl

COPY entrypoint.sh .
RUN chmod +x entrypoint.sh

CMD ./entrypoint.sh
