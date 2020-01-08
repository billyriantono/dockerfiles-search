FROM erblast/r_conda:3.6.1
RUN apt-get update
RUN apt-get install build-essential -y
RUN apt-get install graphviz -y
RUN conda update -n base -c defaults conda
RUN conda install git
RUN apt-get -qq update 
RUN apt-get install -qqy python3-setuptools python3-docutils python3-flask
RUN pip install psutil
RUN conda install datrie
RUN pip install snakemake
RUN pip install networkx pygraphviz
RUN apt install imagemagick -y
RUN pip install pygments
RUN pip install jinja2
