# base image
FROM cognify/rjdbc-base-deb-packages

MAINTAINER Norbert Walchhofer <nw@cognify.ai>

RUN install2.r -l /usr/lib/R/site-library littler \
 && install2.r -e -s -d TRUE tidyr dplyr caret pracma \
 && rm -rf /tmp/downloaded_packages/ /tmp/*.rds

CMD ["/usr/bin/R"]