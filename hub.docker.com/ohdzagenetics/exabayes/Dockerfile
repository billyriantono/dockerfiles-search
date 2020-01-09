#Headers
FROM debian:wheezy

ENV CURRENT_VERSION "1.5"

# Install dependencies
RUN echo "deb http://cran.rstudio.com/bin/linux/debian wheezy-cran3/" >> /etc/apt/sources.list && \
	apt-get update && apt-get install -y --force-yes \
		autoconf \
		autoconf-archive \
		gcc \
		g++ \
		libopenmpi-dev \
		mafft \
		make \
		mpich2 \
		openmpi-bin \
		r-base \
		ruby \
		zip

# Install language additiona
RUN gem install bio && \
	Rscript -e "install.packages('ape', repos='http://cran.us.r-project.org')"

#RAxML
RUN cd
ADD https://github.com/stamatak/standard-RAxML/archive/master.zip master.zip
RUN unzip master.zip
RUN cd standard-RAxML-master && \
	make -f Makefile.AVX.gcc

#ExaML
ADD https://github.com/stamatak/ExaML/archive/master.zip master.zip
RUN unzip master.zip
RUN cd ExaML-master/examl && \
	make -f Makefile.AVX.gcc
RUN cd ExaML-master/parser && \
	make -f Makefile.SSE3.gcc

#ExaBayes
ADD https://sco.h-its.org/exelixis/resource/download/software/exabayes-$CURRENT_VERSION.zip \
	exabayes-$CURRENT_VERSION.zip
RUN unzip exabayes-$CURRENT_VERSION.zip
RUN cd exabayes-$CURRENT_VERSION && ./configure --enable-mpi && \
	make && \
	make install


#Make everything executable
RUN cp /ExaML-master/examl/examl-AVX /bin/examl
RUN cp /ExaML-master/parser/parse-examl /bin/parse-examl

