FROM datasciencedojo/docker62
USER $NB_UID
RUN Rscript -e "install.packages('tensorflow',repos='https://cloud.r-project.org/',dependencies=TRUE)"
RUN Rscript -e "install.packages('keras',repos='https://cloud.r-project.org/',dependencies=TRUE)"
