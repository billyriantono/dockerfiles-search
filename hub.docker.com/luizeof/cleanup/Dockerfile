FROM docker:stable

ENV PRUNE_DELAY=3600

COPY entrypoint.sh /entrypoint.sh

ENTRYPOINT ["/entrypoint.sh"]

CMD ["container", "volume", "network"]
