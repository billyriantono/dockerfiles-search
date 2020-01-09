################# BASE IMAGE ######################
FROM rocker/tidyverse

################## MAINTAINER #####################
LABEL maintainer.name="Max Hargreaves"
LABEL maintainer.email="whargrea@uoguelph.ca"

################# INSTALLATION ####################
RUN BUILDEPS="\
  cargo \
  default-jdk \
  libavfilter-dev \
  libbz2-dev \
  libcurl4-openssl-dev \
  libgdal-dev \
  libgl1-mesa-dev \
  libglu1-mesa-dev \
  libgsl-dev \
  libleptonica-dev \
  libmagick++-dev \
  libpoppler-cpp-dev \
  libudunits2-dev \
  librsvg2-dev \
  libssl-dev \
  libtesseract-dev \
  libxml2-dev \
  tesseract-ocr-eng \
  tk-dev" \
  && apt-get update \
  && apt-get -y --no-install-recommends install $BUILDEPS
   
RUN install2.r --error --deps TRUE \
  ade4 \
  ape \
  adegenet \
  circlize \
  dbscan \
  dendextend \
  extrafont \
  GeneticSubsetter \
  GGally \
  ggrepel \
  igraph \
  import \
  mmod \
  plyr \
  poppr \
  pracma \
  RColorBrewer \
  Rfast \
  roxygen2 \
  scrime \
  vcd \
  && r -e "BiocManager::install('SNPRelate')" \
  && r -e "devtools::install_git('https://github.com/DiDeoxy/PGDA')" \
  && r -e "library(extrafont); font_import(prompt = FALSE); loadfonts()"

RUN apt-get remove --purge -y $BUILDDEPS \
  && apt-get -y --no-install-recommends install default-jre \
  && apt-get autoremove -y \
  && apt-get autoclean -y \
  && rm -rf /var/lib/apt/lists/*

CMD [""]