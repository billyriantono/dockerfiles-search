FROM aguidetti/r-datascience-notebook

MAINTAINER Andrew Guidetti <andrew_Guidetti@hms.harvard.edu>

USER $NB_USER

# https://github.com/hms-dbmi/Rcupcake
# Version: 1.0.1
RUN Rscript -e 'devtools::install_github("hms-dbmi/Rcupcake", force = TRUE)'
