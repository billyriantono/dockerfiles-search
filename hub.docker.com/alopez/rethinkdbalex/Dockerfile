# Se base sur l'image ubuntu version 14.04
FROM ubuntu:14.04

# Met à jour les packages Linux
RUN sed -i.bak 's/main$/main universe/' /etc/apt/sources.list
RUN apt-get update -q
RUN apt-get upgrade -q -y

# Installe software-properties-common
RUN apt-get install -q -y software-properties-common

# Ajoute le repository RethinkDB PPA
RUN add-apt-repository ppa:rethinkdb/ppa
RUN apt-get update -q

# Installe RethinkDB
RUN apt-get --force-yes install -q -y rethinkdb

# Ports à exposer à l’extérieur
EXPOSE 8080 28015 29015

# Crée le volume /rethinkdb
VOLUME ["/rethinkdb"]

# Commandes qui s'éxécutent au démarrage du container
ENTRYPOINT ["/usr/bin/rethinkdb"]
CMD ["--help"]
