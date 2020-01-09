FROM r-base
LABEL description="r image with timeseries packages [tseries, forecast] installed, and also a RServe is started"
LABEL author="reminia.scarlet@gmail.com"
RUN apt-get update
RUN apt-get install libcurl4-openssl-dev
RUN apt-get install curl
WORKDIR /opt/rscripts
COPY rscript.r /opt/rscripts
COPY Rserv.conf /etc/
RUN Rscript rscript.r
EXPOSE 6311
CMD R -e "Rserve::run.Rserve(remote=TRUE)"