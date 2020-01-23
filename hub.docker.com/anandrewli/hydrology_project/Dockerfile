# our base image
FROM conda/miniconda3
#4.7.10

# install packages
RUN conda create -n R3.4 R=3.4
RUN conda install -c r r-caret
RUN conda install -c r r-randomForest

# run the R code
# RUN chmod +x /home/analysis/model_flood_counts_rf_ps_cln_NEW.r
WORKDIR /home/analysis
CMD Rscript /home/analysis/model_flood_counts_rf_ps_cln_NEW.r



