FROM nats:latest

COPY nats.conf nats.conf

ENTRYPOINT ["/gnatsd"]
CMD ["-c", "nats.conf"]