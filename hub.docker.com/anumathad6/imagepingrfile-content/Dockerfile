FROM ubuntu:16.04

ENV SPARK_VERSION=2.4.3
ENV HADOOP_VERSION=2.7
ENV ZEPPELIN_VERSION="0.8.1"

ENV LOG_TAG="[ZEPPELIN_${ZEPPELIN_VERSION}]:" \
    Z_HOME="/zeppelin" \
    LANG=en_US.UTF-8 \
    LC_ALL=en_US.UTF-8

RUN apt-get -y update && \
    apt-get install -y locales && \
    locale-gen $LANG && \
    apt-get install -y software-properties-common && \
    apt -y autoclean && \
    apt -y dist-upgrade && \
    apt-get install -y build-essential

RUN apt-get install -y wget curl grep sed dpkg && \
    TINI_VERSION=`curl https://github.com/krallin/tini/releases/latest | grep -o "/v.*\"" | sed 's:^..\(.*\).$:\1:'` && \
    curl -L "https://github.com/krallin/tini/releases/download/v${TINI_VERSION}/tini_${TINI_VERSION}.deb" > tini.deb && \
    dpkg -i tini.deb && \
    rm tini.deb

ENV JAVA_HOME=/usr/lib/jvm/java-8-openjdk-amd64
RUN apt-get -y update && \
    apt-get install -y openjdk-8-jdk && \
    rm -rf /var/lib/apt/lists/*

RUN apt-get -y update && \
    apt-get install -y bzip2 ca-certificates \
    libglib2.0-0 libxext6 libsm6 libxrender1 \
    git mercurial subversion && \
    echo 'export PATH=/opt/conda/bin:$PATH' > /etc/profile.d/conda.sh && \
    wget --quiet https://repo.continuum.io/miniconda/Miniconda2-4.2.12-Linux-x86_64.sh -O ~/miniconda.sh && \
    /bin/bash ~/miniconda.sh -b -p /opt/conda && \
    rm ~/miniconda.sh
ENV PATH /opt/conda/bin:$PATH

RUN apt-get -y update && \
    apt-get install -y python-dev python-pip && \
    apt-get install -y gfortran && \
    # numerical/algebra packages
    apt-get install -y libblas-dev libatlas-dev liblapack-dev && \
    # font, image for matplotlib
    apt-get install -y libpng-dev libfreetype6-dev libxft-dev && \
    # for tkinter
    apt-get install -y python-tk libxml2-dev libxslt-dev zlib1g-dev && \
    conda config --set always_yes yes --set changeps1 no && \
    conda update -q conda && \
    conda info -a && \
    conda config --add channels conda-forge && \
    conda install -q numpy=1.12.1 scipy=1.2.1 pandas=0.21.1 matplotlib=2.1.1 pandasql=0.7.3 ipython=5.4.1 jupyter_client=5.1.0 ipykernel=4.7.0 bokeh=0.12.10 && \
    pip install -q ggplot==0.11.5 grpcio==1.8.2 bkzep==0.4.0

# R support
# RUN echo "deb http://cran.rstudio.com/bin/linux/ubuntu xenial/" | tee -a /etc/apt/sources.list && \
#     gpg --keyserver keyserver.ubuntu.com --recv-key E084DAB9 && \
#     gpg -a --export E084DAB9 | apt-key add - && \
#     apt-get -y update && \
#     apt-get -y install r-base r-base-dev && \
#     R -e "install.packages('knitr', repos='http://cran.us.r-project.org')" && \
#     R -e "install.packages('ggplot2', repos='http://cran.us.r-project.org')" && \
#     R -e "install.packages('googleVis', repos='http://cran.us.r-project.org')" && \
#     R -e "install.packages('data.table', repos='http://cran.us.r-project.org')" && \
#     # for devtools, Rcpp
#     apt-get -y install libcurl4-gnutls-dev libssl-dev && \
#     R -e "install.packages('devtools', repos='http://cran.us.r-project.org')" && \
#     R -e "install.packages('Rcpp', repos='http://cran.us.r-project.org')" && \
#     Rscript -e "library('devtools'); library('Rcpp'); install_github('ramnathv/rCharts')"

RUN wget -O /tmp/zeppelin-${ZEPPELIN_VERSION}-bin-all.tgz http://archive.apache.org/dist/zeppelin/zeppelin-${ZEPPELIN_VERSION}/zeppelin-${ZEPPELIN_VERSION}-bin-all.tgz && \
    tar -zxvf /tmp/zeppelin-${ZEPPELIN_VERSION}-bin-all.tgz && \
    rm -rf /tmp/zeppelin-${ZEPPELIN_VERSION}-bin-all.tgz && \
    mv /zeppelin-${ZEPPELIN_VERSION}-bin-all ${Z_HOME}

# facilities
RUN pip install -q --upgrade pip
RUN pip install -q neo4j scikit-learn py2neo

RUN wget --no-verbose http://apache.mirror.iphh.net/spark/spark-${SPARK_VERSION}/spark-${SPARK_VERSION}-bin-hadoop${HADOOP_VERSION}.tgz && tar -xvzf spark-${SPARK_VERSION}-bin-hadoop${HADOOP_VERSION}.tgz \
      && mv spark-${SPARK_VERSION}-bin-hadoop${HADOOP_VERSION} /spark \
      && rm spark-${SPARK_VERSION}-bin-hadoop${HADOOP_VERSION}.tgz

ENV SPARK_HOME=/spark

RUN apt-get autoclean && \
    apt-get clean

EXPOSE 8080

ENTRYPOINT [ "/usr/bin/tini", "--" ]

WORKDIR ${Z_HOME}

CMD ["bin/zeppelin.sh"]