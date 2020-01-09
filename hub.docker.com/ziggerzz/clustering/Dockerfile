# Docker settings: Ubuntu, Python3, pip, general machine learning frameworks, Jupyter Notebook.

FROM jupyter/datascience-notebook:latest

LABEL maintainer="Zigfrid Zvezdin ziggerzz@gmail.com>"

# Copy sample notebooks.
COPY notebooks /notebooks

WORKDIR /notebooks

# Install machine learning packages.
# RUN pip install nltk gensim==3.7.3 pyldavis

## RUN pip install pipenv==2018.11.26

## COPY Pipfile Pipefile.lock ./

## RUN PIPENV_VENV_IN_PROJECT=1 pipenv install

## RUN pipenv run python -c "import nltk; nltk.download('stopwords'); nltk.download('punkt')"

# RUN python -c "import nltk; nltk.download('stopwords'); nltk.download('punkt')"
