FROM mcfonsecalab/python27_bio:latest

MAINTAINER Pedro Barbosa <pedro.barbosa@medicina.ulisboa.pt>

WORKDIR /tools
RUN apt-get install -y libcurl4-openssl-dev libssl-dev libgsl-dev liblapack-dev gfortran
#RUN ln /usr/lib/x86_64-linux-gnu/libgsl.so.19 /usr/lib/x86_64-linux-gnu/libgsl.so.0
ADD dependencies.txt /tmp/dependencies.txt
RUN conda install --yes --file /tmp/dependencies.txt 

RUN conda update --all 
RUN git clone https://github.com/davidaknowles/leafcutter && cd leafcutter
RUN R -e "install.packages(c('devtools','shinyjs','rstantools'),repos='http://cran.us.r-project.org')"
RUN cd leafcutter &&  R CMD INSTALL --build leafcutter
ENV leafcutter="/tools/leafcutter"
ENV PATH="${leafcutter}/scripts:${leafcutter}/clustering:$PATH"
