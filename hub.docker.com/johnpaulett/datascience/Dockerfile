# ad3574d3c5c7 latest in November 2019
FROM jupyter/tensorflow-notebook:ad3574d3c5c7

COPY requirements.txt $HOME/requirements.txt
RUN pip install --require-hashes -r $HOME/requirements.txt
RUN python -m nltk.downloader all
