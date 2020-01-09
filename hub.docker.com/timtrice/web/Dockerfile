FROM rocker/tidyverse:3.4.4

# Update system software
RUN apt-get update \
  && apt-get install -y \
    # For rrricanes
    libgdal-dev \
    libproj-dev \
    # For the littler R package
    r-cran-littler \
    # These next two are for XLConnect (a dependency of tidyquant)
    openjdk-8-jdk \
    # Database drivers
    unixodbc  \
    unixodbc-dev \
    tdsodbc \
    odbc-postgresql \
    libsqliteodbc \
    # Needed to add the Microsoft sources below.
    apt-transport-https \
    # This is for me.
    vim \
    curl \
    # For MS SQL Server \ need to install ODBC 13 Driver (17 not avail as of now).
  && curl https://packages.microsoft.com/keys/microsoft.asc | apt-key add - \
  && curl https://packages.microsoft.com/config/debian/8/prod.list > /etc/apt/sources.list.d/mssql-release.list \
  && apt-get update \
  && ACCEPT_EULA=Y apt-get install msodbcsql \
  # Set java conf
  && R CMD javareconf \
  && install2.r -e \
    blogdown \
    corrplot \
    ggrepel \
    HURDAT \
    miniUI \
    packrat \
    pander \
    PKI \
    RCurl \
    RJSONIO \
    rnaturalearthdata \
    rsconnect \
    skimr \
    sweep \
    tibbletime \
    tidyquant \
    timetk \
  && install2.r -e -r https://timtrice.github.io/drat/ \
    rrricanesdata \
  && installGithub.r \
    r-dbi/DBI \
    r-dbi/odbc \
    r-dbi/RMariaDB \
    r-dbi/RPostgres \
    ropensci/rrricanes \
    timtrice/NCDCStormEvents \
    yihui/xfun \
  && echo "\n# set CRAN mirrors \
    \noptions('repos' = c(getOption('repos'), \
    \n\t\t\t\t\t\t\t\t\t\t'https://timtrice.github.io/drat/'), \
    \n\t\t\t\t'blogdown.hugo.dir' = '/home/rstudio/bin/', \
    \n\t\t\t\t'warnPartialMatchArgs' = TRUE,  \
    \n\t\t\t\t'warnPartialMatchDollar' = TRUE, \
    \n\t\t\t\t'warnPartialMatchAttr' = TRUE) \
    \n" >> /usr/local/lib/R/etc/Rprofile.site \
  && R -e "blogdown::install_hugo()" \
  && chown -R rstudio:rstudio /home/rstudio/bin
