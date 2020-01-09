# FROM indicarem a partir de quina image generem la nova
FROM r-base

RUN install2.r --error --deps TRUE  Rcpp
RUN install2.r -r http://bioconductor.org/packages/3.0/bioc --deps TRUE \
	BiocInstaller \	
	affy \
	affydata \
	graph \
	aroma.affymetrix \	

    rm -rf /tmp/downloaded_packages

