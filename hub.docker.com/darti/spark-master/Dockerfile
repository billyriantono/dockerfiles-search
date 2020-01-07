FROM darti/spark

MAINTAINER darti

WORKDIR /usr/local/spark

EXPOSE 8080 7077

CMD tail -f $(./sbin/start-master.sh | sed 's/\(.*\)logging to \(.*\)/\2/')
