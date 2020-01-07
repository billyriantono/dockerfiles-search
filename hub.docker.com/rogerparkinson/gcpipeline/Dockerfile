FROM google/cloud-sdk:latest
LABEL Description="Contains GC tools as well as Java8 and maven. Used in bitbucket pipelines"
VOLUME /tmp
RUN apt-get install -yq apt-utils && apt-get install -yq maven && apt-get install -yq zip && apt-get install -yq gettext-base
