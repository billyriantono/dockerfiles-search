FROM continuumio/anaconda3

RUN conda install scrapy
RUN conda install pymongo
ADD requirements.txt requirements.txt
RUN pip install -r requirements.txt
RUN pip install docx-mailmerge
VOLUME ["/home"]
