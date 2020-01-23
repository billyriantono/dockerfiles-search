FROM ubuntu:16.04
MAINTAINER a504082002 <a504082002@gmail.com>

RUN apt-get update -qq && \
	apt-get install -yq --no-install-recommends \
						wget && \
	apt-get clean && \
	rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

RUN	wget --no-check-certificate https://julialang-s3.julialang.org/bin/linux/x64/0.6/julia-0.6.1-linux-x86_64.tar.gz && \
	tar zxvf julia-0.6.1-linux-x86_64.tar.gz && \
	rm julia-0.6.1-linux-x86_64.tar.gz && \
	export PATH=$PATH:julia-0d7248e2ff/bin && \
	julia -e 'Pkg.update(); Pkg.add("DataFrames"); Pkg.add("InformationMeasures"); using DataFrames; using InformationMeasures'

CMD ["bash"]
