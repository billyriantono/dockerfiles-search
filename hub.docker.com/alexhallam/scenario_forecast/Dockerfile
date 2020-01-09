# FROM alexhallam/tidybayes:3.5.0
FROM alexhallam/tidybayes:3.5

# install the linux libraries needed for plumber
RUN apt-get update -qq && apt-get install -y \
  libssl-dev \
  libcurl4-gnutls-dev 
  
# install plumber
RUN R -e "install.packages('plumber')"
RUN R -e "install.packages('devtools')"
RUN R -e "install.packages('cfsalesdata1', repos = 'https://alexhallam.github.io/drat/', type = 'source')"

# copy everything from the current directory into the container
COPY / /

# open port 80 to traffic
EXPOSE 8000

# when the container starts, start the main.R script
ENTRYPOINT ["Rscript", "main.R"]
