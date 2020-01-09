FROM docker:18-dind

ENV DIND_SHARED_VOLUMES ""

COPY entrypoint.sh /entrypoint.sh
RUN chmod +x /entrypoint.sh

ENTRYPOINT ["/entrypoint.sh"]
