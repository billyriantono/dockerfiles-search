FROM r-base:3.5.0
MAINTAINER garyli@email.arizona.edu

# updates shell
RUN apt-get update

# Installs pandoc, libcurl, libxml2, libxslt1, and libssl
RUN apt-get install -y pandoc \
libcurl4-openssl-dev \
libxml2-dev \
libxslt1-dev \
libssl-dev

# Installs biolite
# Which is needed to insall the bioconductor package edgeR
# to perform differential expression analysis
RUN Rscript -e 'source("https://bioconductor.org/biocLite.R")' \ 
				'biocLite("DESeq2")'

# Installs devtools
Run Rscript -e 'install.packages(c("devtools","getopt"))'

# Installs LncPipeReporter
Run Rscript -e 'devtools::install_github("bioinformatist/LncPipeReporter")'

# Copy the wrapper script inside the container
COPY lncreporter_wrapper.R /usr/bin
RUN chmod +x /usr/bin/lncreporter_wrapper.R

# CMD
ENTRYPOINT ["lncreporter_wrapper.R"]
