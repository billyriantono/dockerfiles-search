FROM trestletech/plumber
USER docker
WORKDIR /home/docker
RUN R -e "install.packages('dplyr')"
CMD ["app/titanic-api.R"]
