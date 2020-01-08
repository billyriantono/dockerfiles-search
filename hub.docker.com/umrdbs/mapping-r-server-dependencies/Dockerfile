# Mapping Dependencies Image
FROM umrdbs/mapping-dependencies:latest AS builder

# Setup directories
WORKDIR /app
COPY scripts /app/install

# R packages to install
ARG RPACKAGES='"caret","ggplot2","randomForest","raster","sp"'
ENV RPACKAGES ${RPACKAGES}

# Install Dependencies
RUN apt-get update && \
    apt-get install --yes r-cran-rcpp && \
    wget --no-verbose https://cran.r-project.org/src/contrib/Archive/RInside/RInside_0.2.13.tar.gz && \
    tar -xvf RInside_0.2.13.tar.gz
COPY scripts/RInsideConfig.h RInside/inst/include/RInsideConfig.h
RUN R CMD INSTALL RInside
RUN R -e 'install.packages(c('$RPACKAGES'), repos="http://cran.us.r-project.org", Ncpus='$(cat /proc/cpuinfo | grep processor | wc -l)')'

# Update System, Clean up Scripts and APT when done.
RUN apt-get update && \
    apt-get upgrade -y -o Dpkg::Options::="--force-confold" && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* && \
    rm -rf /app/install

