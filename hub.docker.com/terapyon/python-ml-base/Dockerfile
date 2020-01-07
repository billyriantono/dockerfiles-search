FROM python:3.6
MAINTAINER "Manabu TERADA" <terada@cmscom.jp>

RUN apt-get update -y
RUN apt-get install -y build-essential libssl-dev libxml2-dev libxslt1-dev 
RUN apt-get install -y libbz2-dev zlib1g-dev libreadline-gplv2-dev
RUN apt-get install -y libblas-dev liblas-dev liblapack-dev gfortran 
RUN apt-get install -y libfreetype6-dev libjpeg62-turbo-dev

RUN pip install numpy scipy pandas scikit-learn matplotlib
RUN pip install ipython[notebook]

COPY requirements.txt requirements.txt
RUN pip install -r requirements.txt
#CMD ["/bin/bash"]

