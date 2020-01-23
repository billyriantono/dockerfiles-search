FROM rocker/r-ver:3.5.3

RUN apt-get update -qq && apt-get install -y \
  curl \
  apt-transport-https \
  git-core \
  libssl-dev \
  libcurl4-gnutls-dev \
  libmariadbclient-dev \
  libpq-dev \
  libssl-dev \
  libxml2-dev \
  unixodbc-dev \
  gnupg2 \
  && curl https://packages.microsoft.com/keys/microsoft.asc | apt-key add - \
  && curl https://packages.microsoft.com/config/debian/9/prod.list > /etc/apt/sources.list.d/mssql-release.list \
  && apt-get update \
  && ACCEPT_EULA=Y apt-get install -y msodbcsql17 mssql-tools

RUN install2.r \
  --deps TRUE \
  --error \
  caret \
  dplyr \
  purrr \
  RecordLinkage \
  plumber \
  odbc \
  tidyr \
  openxlsx \
  stringr

EXPOSE 8000
ENTRYPOINT ["R", "-e", "pr <- plumber::plumb(commandArgs()[6]); pr$run(host='0.0.0.0', port=8000, swagger = TRUE)"]
CMD ["/usr/local/lib/R/site-library/plumber/examples/04-mean-sum/plumber.R"]
