FROM jupyter/datascience-notebook

USER root
RUN apt-get update && \
    apt-get install -y --no-install-recommends \
    libpq-dev postgresql

USER $NB_UID
RUN pip install sqlalchemy psycopg2 plotly seaborn voila nbconvert tensorflow==2.0.0 virtualenv
