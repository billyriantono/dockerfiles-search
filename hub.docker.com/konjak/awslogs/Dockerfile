FROM alpine
RUN apk add python py-pip --no-cache \
 && pip install awslogs
ENTRYPOINT ["awslogs"]
CMD ["-h"]
