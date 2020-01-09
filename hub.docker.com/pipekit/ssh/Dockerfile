FROM alpine:latest
RUN apk --no-cache add openssh-client
ADD config /root/.ssh/config
RUN chmod 400 /root/.ssh/config
CMD ["ssh"]
