FROM redis

COPY entrypoint.sh /usr/local/bin/
COPY redis.conf /usr/local/etc/

EXPOSE 6379
EXPOSE 16379

ENTRYPOINT ["/usr/local/bin/entrypoint.sh"]
CMD ["redis-server", "/usr/local/etc/redis.conf"]
