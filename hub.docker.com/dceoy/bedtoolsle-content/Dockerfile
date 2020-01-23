FROM datasciencedojo/docker67
USER $NB_UID
RUN Rscript -e "install.packages('sentimentr',repos='http://cran.us.r-project.org', dependencies=TRUE)"
RUN Rscript -e "install.packages('sendmailR',repos='http://cran.us.r-project.org', dependencies=TRUE)"
