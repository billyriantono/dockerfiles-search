FROM inwt/r-batch:3.5.1
RUN Rscript -e "install.packages(c('devtools', 'covr'))"
ADD covr.R /includes/
ADD lintr.R /includes/
RUN chmod +x /includes/*.R \
    && ln -s /includes/covr.R /usr/local/bin/covr \
	&& ln -s /includes/lintr.R /usr/local/bin/lintr