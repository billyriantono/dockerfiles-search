############################################################
# Dockerfile for a Scrapy development environment
# Based on Ubuntu Image
############################################################

FROM ubuntu
MAINTAINER NeuralFoundry <neuralfoundry.com>

# RUN echo deb http://archive.ubuntu.com/ubuntu precise universe >> /etc/apt/sources.list
RUN apt-get update

## Python Family
RUN apt-get install -qy python3 python3-dev python-distribute python3-pip ipython

## Selenium 
RUN apt-get install -qy firefox xvfb 
RUN pip3 install selenium pyvirtualdisplay

## AWS Python SDK
RUN pip3 install boto3

## Scraping
RUN pip3 install beautifulsoup4 requests 
RUN apt-get install -qy libffi-dev libxml2-dev libxslt-dev lib32z1-dev libssl-dev

## Scrapy
RUN pip3 install lxml scrapy scrapyjs
