FROM ubuntu:bionic

RUN apt-get update
RUN apt-get install -y curl
COPY entrypoint.sh /usr/local/bin/
ENTRYPOINT ["/usr/local/bin/entrypoint.sh"]

CMD ["echo Goodbye"]