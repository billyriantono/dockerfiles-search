#
# iRODS Packages Builder Image.
#
FROM ubuntu:16.04

# Install iRODS dependencies.

RUN apt-get update  && \
    apt-get -y install git g++ make python-dev help2man unixodbc libfuse-dev \
                       libcurl4-gnutls-dev libbz2-dev zlib1g-dev lsb-release \
                       libpam0g-dev libssl-dev libxml2-dev libkrb5-dev \
                       unixodbc-dev libjson-perl python-psutil wget \
                       python-jsonschema super python-exif odbc-postgresql

RUN apt-get -y install apt-transport-https postgresql && \
    wget -qO - https://packages.irods.org/irods-signing-key.asc | apt-key add - && \
    echo "deb [arch=amd64] https://packages.irods.org/apt/ $(lsb_release -sc) main" | \
         tee /etc/apt/sources.list.d/renci-irods.list && \
    apt-get update

ADD db_commands.txt /

#RUN echo >/start.sh "service postgresql start && su - postgres -c 'psql -f /db_commands.txt' && \\
#    apt-get -y install irods-server irods-database-plugin-postgres && \\
#    python /var/lib/irods/scripts/setup_irods.py \\
#        < /var/lib/irods/packaging/localhost_setup_postgres.input"

ADD start.sh /
RUN chmod u+x /start.sh

#ENTRYPOINT ["/bin/bash"]
#ENTRYPOINT ["/start.sh"]
CMD ["/bin/bash"]
