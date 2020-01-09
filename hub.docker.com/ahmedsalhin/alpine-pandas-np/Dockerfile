FROM nbgallery/jupyter-alpine

LABEL maintainer = "Ahmed.Salhin@sage.com" name= "Alpine with pandas and jupyter" version= "0.1.0"

RUN mkdir -p /usr/src/app

WORKDIR /usr/src/app

RUN pip install --upgrade pip

RUN pip3 install pandas
