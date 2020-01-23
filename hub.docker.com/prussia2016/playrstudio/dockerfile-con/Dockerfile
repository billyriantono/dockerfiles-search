FROM prete/jupyter-rstudio:3.6.2

# Seurat
RUN Rscript -e 'BiocManager::install("multtest")'
RUN Rscript -e 'install.packages(c("Seurat"), dependencies = TRUE)'

# Install additional 
RUN Rscript -e 'install.packages(c("rJava", "Rmagic"), dependencies = TRUE)'
