FROM rocker/geospatial

LABEL maintainer="Aleksei Solovev <lelkaklel@gmail.com>"
LABEL version="1.0.0"

RUN apt-get update \
  && apt-get install -y --no-install-recommends \
    freetds-bin \
    tdsodbc \
  && install2.r --error \
    RODBC \
    caTools

COPY odbcinst.ini /etc/
  
EXPOSE 8787

WORKDIR /home/rstudio

CMD ["/init"]
