FROM		hauptmedia/spark-base

ADD		docker-entrypoint.sh /usr/local/sbin/docker-entrypoint.sh

# TCP   7077    Spark Mater
# TCP   8080    Spark Master WebUI HTTP connector

EXPOSE 7077 8080 

ENTRYPOINT ["/usr/local/sbin/docker-entrypoint.sh"]
