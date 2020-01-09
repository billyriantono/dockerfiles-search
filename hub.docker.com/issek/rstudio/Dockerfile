FROM rocker/tidyverse@sha256:9a652bbfd490ce8e48679345a7ab6d54b5c4b0c8390091ae7f65092755d203b6

# install basic system dependencies
RUN apt-get update && apt-get install -y libgit2-dev && apt-get install -y python3-pip python3.5-dev git \
&& pip3 install --upgrade pip

# install rsvg
RUN apt-get install -y librsvg2-dev
RUN R -e "install.packages('rsvg',dependencies=TRUE, repos='http://cran.rstudio.com/')"

# install other R packages
RUN R -e "install.packages('reticulate',dependencies=TRUE, repos='http://cran.rstudio.com/')"
RUN R -e "install.packages('shiny',dependencies=TRUE, repos='http://cran.rstudio.com/')"

# install python libraries
RUN pip3 install pandas requests lxml fastcluster scipy sklearn spacy