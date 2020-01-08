## Start with the official tidyverse rocker image (lightweight Debian)
FROM rocker/tidyverse:latest

MAINTAINER tynor88 <tynor@hotmail.com>

## Install Java
RUN apt-get update && apt-get install -y \
default-jdk \
## used to build rJava and other packages
libbz2-dev \
libicu-dev \
liblzma-dev

## Install rJava package
RUN install2.r --error \
rJava \
  && rm -rf /tmp/downloaded_packages/ /tmp/*.rds
  
