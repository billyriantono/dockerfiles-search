FROM couchdb:2.1.1
ARG DEBIAN_FRONTEND=noninteractive
RUN apt-get update && apt-get install -y --no-install-recommends apt-utils && apt-get install apt-file -y && apt-file update && apt-get install vim -y
ADD local.ini /opt/couchdb/etc/local.d/local.ini
