FROM erblast/r_conda_snakemake:3.6.0
RUN R -e "remotes::install_version('easyalluvial', version = '0.2.0', repos='http://cran.us.r-project.org')"
RUN git clone -b v0.0.0.9001 --single-branch https://github.com/erblast/pipelearner.git pipelearner 
RUN R -e "devtools::install('pipelearner/')"
RUN rm pipelearner/ -r
RUN git clone -b v0.2.14 --single-branch https://github.com/erblast/oetteR.git oetteR 
RUN R -e "devtools::install('oetteR/')"
RUN R -e "remotes::install_version('rsample', repos='http://cran.us.r-project.org', version= '0.0.5')"
RUN R -e "remotes::install_version('yardstick', repos='http://cran.us.r-project.org', version = '0.0.4')"
RUN R -e "remotes::install_version('parsnip', repos='http://cran.us.r-project.org', version = '0.0.3.1' )"
RUN R -e "remotes::install_version('tidyr', repos='http://cran.us.r-project.org', version = '0.8.3' )"
RUN R -e "devtools::test('oetteR/')"
RUN rm oetteR/ -r
