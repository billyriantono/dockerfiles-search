FROM r-base:3.5.0
LABEL maintainer="Florian Lahn (florian.lahn@uni-muenster.de)"
LABEL version="0.0.1"
LABEL description="openeo R UDF webservice implementation"
LABEL author1="Florian Lahn (florian.lahn@uni-muenster.de)" \
      author2="Pramit Ghosh (pramitghosh@uni-muenster.de)"

# create the path for the user files
RUN mkdir -p /opt/dockerfiles/

COPY ./ /opt/dockerfiles/

# run commands to prepare the image
# install dependencies
# RUN apt-get -y update && apt-get -y install libgdal-dev libcurl4-gnutls-dev libssl-dev libssh2-1-dev libsodium-dev gdal-bin libudunits2-dev
RUN apt-get update -qq && apt-get install -y \
  libxml2-dev \
  libssl-dev \
  libcurl4-gnutls-dev \
  libudunits2-dev \
  libgdal-dev \
  gdal-bin \
  libgeos++-dev \
  libgeos-c1v5

# libxml2-dev libssl-dev libcurl4-gnutls-dev to get plumber running
# libunits2-dev for stars and sf (gdal is required for sf)

# install R dependencies and install package
RUN R --no-save -f /opt/dockerfiles/docker/install_package_with_dependencies.R



# cmd or entrypoint for startup
ENTRYPOINT ["R", "-q", "--no-save", "-f /opt/dockerfiles/docker/server_start.R"]

EXPOSE 8010
