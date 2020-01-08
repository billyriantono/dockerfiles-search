FROM busybox

ADD /prometheus-puppetdb.yml /
COPY /docker-entrypoint.sh /

ENTRYPOINT ["/docker-entrypoint.sh"]
CMD ["/bin/cp", "-f", "/prometheus-puppetdb.yml", "/etc/prometheus/conf.d/"]
