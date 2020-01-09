FROM rocker/verse:3.4.4
  
#MetaData
LABEL version="1.0"
LABEL software="Lp serogroup prediction custom R scripts and ML model"
LABEL software.version="1.0"
LABEL description="Custom R scripts to assist with Lp serogroup prediction from WGS"
LABEL website="Please refer to GitHub Page for more information - SMorrison42/bioinformaticsDockerContainers"

#Maintainer
MAINTAINER Shatavia Morrison <smorrison@cdc.gov>

#Install Random Forest Package from CRAN with dependencies
RUN R -e "install.packages('randomForest', dependencies=TRUE,repos = 'http://cran.us.r-project.org')"

#Install Caret Package from CRAN with dependencies
RUN R -e "install.packages('caret', dependencies=TRUE , repos = 'http://cran.us.r-project.org')"

#Copy R script and model file configured by SSM to file location for Docker
COPY /lpSerogroupRscripts_v1/rScriptsMetaData/*  /scripts/

#Docker run command for R model need increase ulimit size to prevent C stack error
CMD ["Rscript","--max-ppsize=500000", "--verbose", "/scripts/R_modelPredict_version_0.1_20180904Model.R", "/t/modelSitesForRF_Leg54-MKI-D1079-709508_S8_.csv", "D1079", "/t/"]
