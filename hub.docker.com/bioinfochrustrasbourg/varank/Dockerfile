FROM centos:7
MAINTAINER Vincent Zilliox <vzilliox@chru-strasbourg.fr>

##########################################################################
# Dockerfile Version:	1.0
# Software:		VARANK
# Software Version:	1.4.3
# Software Website:	www.lbgi.fr/VaRank
# Description:		Dockerfile to build VARANK container images
##########################################################################


#######
# YUM #
#######

RUN yum -y install wget \
	tcl tcl-devel



##########
# VARANK #
##########

ENV VARANK=/VaRank_1.4.3
RUN wget www.lbgi.fr/VaRank/Sources/VaRank_1.4.3.tar.gz; \
	tar -xzvf VaRank_1.4.3.tar.gz;


ENV PATH="/VaRank_1.4.3/bin:$PATH"

ENTRYPOINT ["VaRank"]
CMD ["--help"]
