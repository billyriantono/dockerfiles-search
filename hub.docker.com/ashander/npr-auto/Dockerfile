FROM ashander/phenoecosim:latest
# includes devtools, rcpp, rcpparmadillo

MAINTAINER Jaime Ashander "jashander@ucdavis.edu"

# use devtools ok
# change entries in the version

RUN Rscript -e "devtools::install_version('cowplot', version='0.5.0', repos='http://cran.us.r-project.org')" \
   && Rscript -e "devtools::install_version('directlabels', version='2013.6.15', repos='http://cran.us.r-project.org')" \
   && Rscript -e "devtools::install_version('dplyr', version='0.4.3', repos='http://cran.us.r-project.org')" \
   && Rscript -e "devtools::install_version('ggplot2', version='1.0.0', repos='http://cran.us.r-project.org')" \
   && Rscript -e "devtools::install_version('gridExtra', version='2.0.0', repos='http://cran.us.r-project.org')" \
   && Rscript -e "devtools::install_version('knitr', version='1.12.3', repos='http://cran.us.r-project.org')" \
   && Rscript -e "devtools::install_version('matrixcalc', version='1.0-3', repos='http://cran.us.r-project.org')" \
   && Rscript -e "devtools::install_version('reshape2', version='1.4.1', repos='http://cran.us.r-project.org')" \
   && Rscript -e "devtools::install_version('plyr', version='1.8.3', repos='http://cran.us.r-project.org')" \
   && rm -rf /tmp/downloaded_packages/ /tmp/*.rds
