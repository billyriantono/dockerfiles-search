FROM redmine:4.0.5-passenger

COPY docker-entrypoint.sh /
ENTRYPOINT ["/docker-entrypoint.sh"]

CMD ["passenger", "start"]
