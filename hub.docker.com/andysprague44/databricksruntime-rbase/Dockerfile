FROM databricksruntime/standard:latest

# Adapted image from databricksruntime/rbase:
# Installs R 3.6.0, avoiding a firewall issue with signing apt for some users
# Installs rstan

RUN apt-get update \
  && apt-get install --yes software-properties-common \
# Ubuntu 16.04.3 LTS installs R version 3.2.3 by default. This is fairly out dated.
# Add RStudio's debian source to enable install r version 3.6.0
  && add-apt-repository 'deb http://cran.rstudio.com/bin/linux/ubuntu xenial-cran35/' \
# Sign it with the more secure pgp key ID as per: https://cran.rstudio.com/bin/linux/ubuntu/#secure-apt (avoiding firewall issues)
  && gpg --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys E298A3A825C0D65DFD57CBB651716619E084DAB9 \
  && gpg -a --export E298A3A825C0D65DFD57CBB651716619E084DAB9 | sudo apt-key add - \
# Update R version (to 3.6.0)
  && apt-get update && apt-get upgrade --yes \
  && apt install --yes r-base r-base-dev libssl-dev

# hwriterPlus is used by Databricks to display output in notebook cells
# Rserve allows Spark to communicate with a local R process to run R code
RUN R -e "install.packages('hwriterPlus', repos='https://mran.revolutionanalytics.com/snapshot/2017-02-26')"
RUN R -e "install.packages('Rserve', repos='http://rforge.net/')"

# Install rstan pre-reqs
RUN mkdir -p ~/.R \
  && echo "CXX14 = g++ -std=c++1y -Wno-unused-variable -Wno-unused-function -fPIC" >> ~/.R/Makevars \
  && apt-get update --yes \
  && apt-get install --yes build-essential libxml2-dev libcurl4-openssl-dev libssl-dev

# Install rstan
# **WARNING**: Ensure docker engine has minimum 4 Gb memory, and 2 Gb swap space, or will hit compiler error
RUN Rscript --no-site-file --slave --no-save --no-restore-history -e "install.packages('rstan', repos='https://cloud.r-project.org/', dependencies=TRUE)"

# Tidy-up
RUN add-apt-repository -r 'deb http://cran.rstudio.com/bin/linux/ubuntu xenial-cran35/' \
  && apt-key del E298A3A825C0D65DFD57CBB651716619E084DAB9 \
  && apt-get clean \
  && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*
