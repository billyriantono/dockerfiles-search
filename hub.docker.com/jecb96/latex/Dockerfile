FROM ubuntu:rolling

ADD 01_nodoc /etc/dpkg/dpkg.cfg.d/01_nodoc

RUN apt-get update && \
    DEBIAN_FRONTEND=noninteractive apt-get install  -y  \
    texlive-full \
	biber \
	curl \
	gnuplot \
	make && \
	apt-get --purge -y remove tex.\*-doc$ && \
  	apt-get clean && \
  	rm -rf /var/lib/apt/lists/*
  
  
# add included latexmk version
ADD latexmk.pl /usr/bin/latexmk
RUN chmod +x /usr/bin/latexmk
