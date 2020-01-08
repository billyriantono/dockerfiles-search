FROM melioconsulting/jupyterlab-data-wrangling:latest
LABEL maintainer='Merelda Wu'

USER root

RUN pip install spaCy pympler nltk gensim rake-nltk pyLDAvis --trusted-host pypi.org --trusted-host files.pythonhosted.org
RUN python -m spacy download en

