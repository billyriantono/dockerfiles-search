## Start with the tidyverse docker image
FROM rocker/tidyverse:3.5.0

MAINTAINER "Sam Abbott" contact@samabbott.co.uk


## Get JAVA
RUN apt-get update -qq \
  && apt-get -y --no-install-recommends install \
    default-jdk \
    default-jre \
  && R CMD javareconf
  
ADD . /home/rstudio/AnalysisSkeleton

WORKDIR /home/rstudio/AnalysisSkeleton

RUN Rscript -e 'install.packages("packrat"); packrat::restore()'
