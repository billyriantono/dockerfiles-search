# Docker file for ecom_analysis
# Veronique Mulholland, Dec 2017

# Usage: This file is used to create the container to run the analysis

# use rocker/hadleyverse as the base image and
FROM rocker/hadleyverse

# get OS updates and install build tools
RUN apt-get update
RUN apt-get install -y build-essential

# install wget and git
RUN apt-get install -y wget
RUN apt-get install -y make git

# packages
#RUN Rscript -e "install.packages('rmarkdown', repos = 'http://cran.us.r-project.org')"
# packages
#RUN Rscript -e "install.packages('tidyr', repos = 'http://cran.us.r-project.org')"
# packages
#RUN Rscript -e "install.packages('magrittr', repos = 'http://cran.us.r-project.org')"
# packages
#RUN Rscript -e "install.packages('data.table', repos = 'http://cran.us.r-project.org')"
# packages
#RUN Rscript -e "install.packages('ggplot2', repos = 'http://cran.us.r-project.org')"
# packages
#RUN Rscript -e "install.packages('dplyr', repos = 'http://cran.us.r-project.org')"
