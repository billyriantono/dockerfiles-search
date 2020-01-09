FROM mcr.microsoft.com/azure-functions/python:2.0

RUN apt-get update && \
    apt-get install -y --no-install-recommends apt-utils  && \
    apt-get install -y antiword && \
    apt-get install -y tesseract-ocr && \
    apt-get install -y libtesseract-dev && \
    apt-get install -y imagemagick

ENV AzureWebJobsScriptRoot=/home/site/wwwroot \
    AzureFunctionsJobHost__Logging__Console__IsEnabled=true

COPY . /home/site/wwwroot

RUN cd /home/site/wwwroot && \
    pip install -r requirements.txt