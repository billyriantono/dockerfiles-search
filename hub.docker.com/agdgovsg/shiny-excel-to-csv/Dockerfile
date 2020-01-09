FROM r-base:3.5.0

ENV RPROFILESITE_LOC /usr/lib/R/etc/Rprofile.site
ENV R_LIB_LOC /usr/lib/R/site-library

RUN echo "deb http://ftp.sg.debian.org/debian/ unstable main" > /etc/apt/sources.list \
    && echo "deb http://deb.debian.org/debian unstable main" >> /etc/apt/sources.list \
    && apt-get update \
    && echo 'options(repos = c(CRAN = "https://cran.microsoft.com/snapshot/2018-06-01/"), download.file.method = "libcurl")' >> $RPROFILESITE_LOC \
    && install2.r --error --libloc $R_LIB_LOC \
      readxl \
      shiny \
      shinythemes \
    && mkdir -p /app/exceltocsv \
    # so that we know which port to expose
    && echo "local({options(shiny.port = 3838, shiny.host = '0.0.0.0')})" >> $RPROFILESITE_LOC \
    && apt-get update \
    && rm -rf /var/lib/apt/lists/*

COPY ui.R /app/exceltocsv
COPY server.R /app/exceltocsv

EXPOSE 3838

CMD ["R", "-e", "shiny::runApp('/app/exceltocsv')"]