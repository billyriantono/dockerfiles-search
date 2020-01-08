FROM jupyter/tensorflow-notebook:latest

RUN conda install --yes --quiet psycopg2=2.6* pymysql ipython-sql=0.3*

# FIXME
COPY startup/* .ipython/profile_default/startup/