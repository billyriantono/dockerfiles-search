# base image
FROM cognify/rjdbc-base-r-packages-1

MAINTAINER Norbert Walchhofer <nw@cognify.ai>

RUN install2.r -e -s -d TRUE ggplot2 proxy readr reshape2 smooth RPostgreSQL DBI RJDBC logisticPCA forecast greybox googleCloudStorageR prophet \
 && rm -rf /tmp/downloaded_packages/ /tmp/*.rds
RUN install2.r -e -s -d TRUE DatabaseConnector \
 && rm -rf /tmp/downloaded_packages/ /tmp/*.rds


CMD ["/usr/bin/R"]