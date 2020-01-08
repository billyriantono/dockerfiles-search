FROM google/cloud-sdk:slim

LABEL "Author"="Andrew Kemp <andrew.kemp@ankemp.com>"
LABEL "Version"="1.0"

## Install Node 8.9.x
RUN curl -sL https://deb.nodesource.com/setup_8.x | bash -
RUN apt-get install -y nodejs


## Install gCloud SQL Proxy
ADD https://dl.google.com/cloudsql/cloud_sql_proxy.linux.amd64 /usr/local/bin/cloud_sql_proxy
RUN chmod +x /usr/local/bin/cloud_sql_proxy