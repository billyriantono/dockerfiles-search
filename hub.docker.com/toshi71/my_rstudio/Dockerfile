FROM tokyor/rstudio:latest

MAINTAINER toshi71

# Install packages
RUN apt-get update && apt-get install -y \
  cmake \
  libudunits2-dev \
  libgdal-dev \
  libgeos-dev \
  libproj-dev

CMD ["/init"]
