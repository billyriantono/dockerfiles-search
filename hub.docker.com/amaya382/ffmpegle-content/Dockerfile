FROM rocker/r-ver

RUN R -e "install.packages('packageTry')"

COPY . ~/packageTry/R

WORKDIR ~/packageTry/R

CMD ["Rscript", "packageTry.R"]
