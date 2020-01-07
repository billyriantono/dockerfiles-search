FROM tobby48/spark-common:2.1
MAINTAINER Suk Heo <tobby48@gmail.com>

# Add custom files, set permissions
ADD entrypoint.sh /usr/local/bin/
RUN chmod +x /usr/local/bin/entrypoint.sh
RUN ln -s usr/local/bin/entrypoint.sh

# TCP   8081    Spark Worker WebUI HTTP connector
EXPOSE 8081

ENTRYPOINT ["entrypoint.sh"]
