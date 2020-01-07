FROM ubuntu:18.04

RUN apt-get update 

RUN apt-get -y install libc-dev

# Basic Ubuntu Dependencies  
RUN apt-get install -y curl python3 python3-pip python-dev build-essential \
                 python3-dev python3-setuptools
                
# Jupyter
RUN pip3 install --upgrade pip setuptools

# General data processing
RUN pip3 install pandas numpy 

# Statistical computation
RUN pip3 install scipy 

# Cloud API access
RUN pip3 install boto3 

# Read Excel files
RUN pip install xlrd

# Natural language processing
RUN pip3 install nltk gensim

# Download NLTK Stopwords
RUN python3 -m nltk.downloader -d /usr/share/nltk_data stopwords
 
