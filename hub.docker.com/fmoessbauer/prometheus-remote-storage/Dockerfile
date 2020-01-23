FROM ubuntu:16.04

MAINTAINER Felix Moessbauer

COPY remote_storage_adapter /
RUN chmod 755 /remote_storage_adapter

EXPOSE 9201
ENTRYPOINT ["./remote_storage_adapter"]
CMD ["-h"]
