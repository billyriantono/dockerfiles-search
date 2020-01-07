FROM ubuntu:16.04

LABEL "title"="Python For Science" \
      "description"="Create a container with many important packages to use right away. Check the complete list on https://github.com/dmoliveira/python-for-science" \
      "version"="1.0.0"

RUN apt-get update -y
RUN apt-get install -y python3-pip 
RUN pip3 install -U pip
RUN pip3 install -U scikit-learn
RUN pip3 install -U scikit-learn
RUN pip3 install -U pandas
RUN pip3 install -U ipdb
RUN pip3 install -U ipython
RUN pip3 install -U numpy
RUN pip3 install -U scikit-learn
RUN pip3 install -U gensim
RUN pip3 install -U SolrClient
RUN pip3 install -U xgboost
RUN pip3 install -U graphviz
RUN pip3 install -U beautifulsoup4
RUN pip3 install -U logbook
RUN pip3 install -U jupyter notebook

ENTRYPOINT while true; do echo "Running Python for Science Container..."; sleep 60; done
