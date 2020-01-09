FROM rocker/r-base

RUN apt-get update \ 
	&& apt-get install -y --no-install-recommends \
		libgmp3-dev

RUN Rscript -e "install.packages('hitandrun')"

CMD ["R"] 