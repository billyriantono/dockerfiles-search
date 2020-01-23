FROM rocker/tidyverse:3.4.1

RUN echo "r <- getOption('repos'); r['CRAN'] <- 'http://cran.us.r-project.org'; options(repos = r);" > ~/.Rprofile
ENV R_LIBS_USER=/usr/local/lib/R/site-library

COPY install_r_packages.R /root/install_r_packages.R
RUN chmod +x /root/install_r_packages.R
RUN Rscript --no-save --no-restore ~/install_r_packages.R

# Set working directory
RUN mkdir /home/working \
     && echo "setwd('/home/working')" >> ~/.Rprofile \
     && echo "setwd('/home/working')" >> /etc/R/Rprofile.site

EXPOSE 8787
CMD ["/init"]