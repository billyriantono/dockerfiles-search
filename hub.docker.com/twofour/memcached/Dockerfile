FROM alpine:3.8
EXPOSE 11211
ENV MEMCACHED_MEMORY_LIMIT=64
COPY src /
RUN memcached-setup
USER memcached
HEALTHCHECK CMD memcached-healthcheck
ENTRYPOINT ["memcached-entrypoint"]
CMD ["memcached"]
