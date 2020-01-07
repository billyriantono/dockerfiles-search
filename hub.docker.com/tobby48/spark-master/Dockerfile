FROM tobby48/spark-common:2.1
MAINTAINER Suk Heo <tobby48@gmail.com>

# Add custom files, set permissions
ADD entrypoint.sh /usr/local/bin/
RUN chmod +x /usr/local/bin/entrypoint.sh
RUN ln -s usr/local/bin/entrypoint.sh

# TCP   7077    Spark Mater
# TCP   8080    Spark Master WebUI HTTP connector
EXPOSE 7077 8080 

ENTRYPOINT ["entrypoint.sh"]
