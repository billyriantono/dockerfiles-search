####### Dockerfile #######
FROM derekpowell/rstudio-bayesreg:latest

ENV DEBIAN_FRONTEND noninteractive

RUN apt-get -y --no-install-recommends install \
	libudunits2-dev \
	jags \
&& R --no-restore --no-save -e \
	'BiocManager::install(c("graph","Rgraphviz","RBGL"), update=FALSE)' \
&& install2.r --error --skipinstalled \
	blavaan \
	bnlearn \
	bnstruct \
	geomnet \
	ggnetwork \
	ggraph \
	HydeNet \
	lavaan \
	semPlot \
	simsem \
	tidygraph \
    BiDAG \
&& installGithub.r \
	hadley/multidplyr@0085ded4048d7fbe5079616c40640dbf5982faf2
