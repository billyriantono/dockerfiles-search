FROM opencpu/rstudio

RUN \
  apt-get update && \
  apt-get install -y libdbd-mysql libmysqlclient-dev

RUN echo "r <- getOption('repos'); r['CRAN'] <- 'http://cran.us.r-project.org'; options(repos = r);" > ~/.Rprofile
RUN Rscript -e "install.packages(c('devtools', 'RMySQL', 'dplyr', 'arules', 'tidyr', 'remotes'))"
