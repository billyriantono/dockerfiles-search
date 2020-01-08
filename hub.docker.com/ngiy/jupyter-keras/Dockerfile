FROM jupyter/datascience-notebook
MAINTAINER ngiy

RUN pip install tensorflow
RUN pip install keras
RUN pip install --upgrade pip

ADD data data

CMD start-notebook.sh --NotebookApp.password='sha1:d1790b6a612d:b163515d4fd10c5516477b5c1ed26314d7d6aee9'
