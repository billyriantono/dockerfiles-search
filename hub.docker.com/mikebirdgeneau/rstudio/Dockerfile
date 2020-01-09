FROM rocker/rstudio

RUN apt-get update; apt-get install -y --no-install-recommends \
  libnetcdf-dev \
  libhdf5-dev \
  libproj-dev \
  libgeos++-dev \
  libgeos-dev 

RUN wget https://github.com/jgm/pandoc/releases/download/1.19.1/pandoc-1.19.1-1-amd64.deb; dpkg -i pandoc-1.19.1-1-amd64.deb; rm pandoc-1.19.1-1-amd64.deb

RUN cd /usr/local/; wget http://www.ftp.cpc.ncep.noaa.gov/wd51we/wgrib2/wgrib2.tgz; tar -xzf wgrib2.tgz; cd grib2; make; ln -s /usr/local/grib2/wgrib2/wgrib2 /usr/local/bin

COPY install_packages.R install_packages.R
RUN /usr/bin/Rscript install_packages.R
