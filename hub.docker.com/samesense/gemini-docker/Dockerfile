FROM ubuntu:14.04
MAINTAINER Dan Gaston <daniel.gaston@gmail.com>
RUN sudo apt-get update && apt-get install -y build-essential python git gcc g++ zlib1g-dev wget curl

RUN mkdir /data/
RUN mkdir /tools/
RUN wget https://github.com/arq5x/gemini/raw/master/gemini/scripts/gemini_install.py
RUN python gemini_install.py /tools /data

ENV PATH $PATH:/tools/bin/:/data/anaconda/bin

#RUN git clone https://github.com/arq5x/gemini
#RUN python /gemini/gemini/install-data.py /data/gemini_data/
#RUN gemini update --dataonly --extra cadd_score
#RUN gemini update --dataonly --extra gerp_bp
