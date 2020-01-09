##########################################################################################
# Base image:                                                                            #
# - Python3                                                                              #
#      - ML (pandas, numpy, sklearn, xgboost)                                            #
#      - Visualization (matplotlib, seaborn)                                             #
#      - additional tools (tqdm, pandas utils)                                           #
# - R                                                                                    #
#      - ML (caret, xgboost, rpart, randomForest)                                        #
#      - Visualization (ggplot2)                                                         #
#      - data formats (stringr, lubridate, zoo, timeDate)                                #
#      - data processing (data.table, reshape2, plyr, dplyr, tidyr)                      #
# - Jupyter kernels: Python, R, Bash                                                     #
# - Jupyter extensions                                                                   #
#                                                                                        #
# 01.12.2016                                                                             #
##########################################################################################

FROM ubuntu:16.04

MAINTAINER "Anton Petrov" petrov.anton.k@gmail.com

ENV TERM xterm

# install some tools
RUN apt-get update && \
	apt-get upgrade -y && \
	apt-get install -y cmake unzip zip nano wget curl git net-tools htop

# install python3.5
RUN apt-get install -y python3 python3-pip && \
	pip3 install -U pip

# install Python machine learning tools
RUN apt-get install -y python3-numpy python3-matplotlib python3-pandas && \
	pip install scikit-learn && \
	pip install hyperopt && \
	pip install xgboost
	
# how to instal openmpi version?
RUN	cd /opt && \
 	git clone --recursive --depth=1 https://github.com/Microsoft/LightGBM && \
 	cd LightGBM && \
 	mkdir build && \
 	cd build && \
 	cmake .. && \
 	make -j && \
 	pip install git+https://github.com/ArdalanM/pyLightGBM.git
	
# install Python vis
RUN pip install seaborn && \
	pip install ggplot && \
	pip install wordcloud
	
# install Python other
RUN pip install pandas-summary && \
	pip install prettypandas && \
	pip install tqdm && \
	pip install openpyxl && \
	pip install editdistance && \
	pip install h5py
	
# install Jupyter extensions
RUN pip install jupyter && \
	pip install yapf && \
	pip install https://github.com/ipython-contrib/jupyter_contrib_nbextensions/tarball/master && \
	jupyter contrib nbextension install --user && \
	jupyter nbextensions_configurator enable --user && \
	jupyter nbextension enable --py --sys-prefix widgetsnbextension && \
	jupyter nbextension enable nbextensions_configurator/tree_tab/main && \
	jupyter nbextension enable toc2/main && \
	jupyter nbextension enable spellchecker/main && \
	jupyter nbextension enable codefolding/main && \
	jupyter nbextension enable collapsible_headings/main && \
	jupyter nbextension enable init_cell/main && \
	jupyter nbextension enable code_prettify/code_prettify && \
	jupyter nbextension enable table_beautifier/main && \
	jupyter nbextension enable chrome-clipboard/main && \
	jupyter nbextension enable hide_input_all/main && \
	jupyter nbextension enable python-markdown/main && \
	jupyter nbextension enable freeze/main
	
	
# R
RUN echo "deb http://cran.rstudio.com/bin/linux/ubuntu xenial/" | tee -a /etc/apt/sources.list && \
	gpg --keyserver keyserver.ubuntu.com --recv-key E084DAB9 && \
	gpg -a --export E084DAB9 | apt-key add - && \
	apt-get install -y r-base r-base-dev libssl-dev libcurl4-openssl-dev && \
	echo "r <- getOption('repos'); r['CRAN'] <- 'http://cran.us.r-project.org'; options(repos = r);" > ~/.Rprofile
	
RUN Rscript -e "install.packages('ggplot2')" && \
	Rscript -e "install.packages('caret')" && \
	Rscript -e "install.packages('xgboost')" && \
	Rscript -e "install.packages('rpart')" && \
	Rscript -e "install.packages('randomForest')" && \
	Rscript -e "install.packages('stringr')" && \
	Rscript -e "install.packages(c('lubridate', 'zoo', 'timeDate'))" && \
	Rscript -e "install.packages(c('data.table', 'reshape2', 'plyr', 'dplyr', 'tidyr'))" && \
	Rscript -e "install.packages(c('curl', 'httr'))" && \
	Rscript -e "install.packages(c('repr', 'IRdisplay', 'evaluate', 'crayon', 'pbdZMQ', 'devtools', 'uuid', 'digest'))" && \
	Rscript -e "devtools::install_github('IRkernel/IRkernel')" && \
	Rscript -e "IRkernel::installspec(user = FALSE)"

# Rscript -e "install.packages('forecast')"
# Rscript -e "install.packages('e1071')"
# Rscript -e "install.packages('kknn')"
# Rscript -e "install.packages('shiny')"


# bash kernel
RUN pip install bash_kernel && \
	python3 -m bash_kernel.install


RUN pip list -o | cut --delimiter=" " --fields=1 | xargs --no-run-if-empty pip install -U && \
	apt-get clean && \
    rm -rf /var/lib/apt/lists/*


VOLUME /mnt/data

# 8888 for Jupyter, others are free
# 27017 for MongoDB
EXPOSE 8888 8889 8890 27017

# create jupyter notebook
CMD jupyter notebook --no-browser --port 8888 --ip=0.0.0.0 --notebook-dir=/mnt/data