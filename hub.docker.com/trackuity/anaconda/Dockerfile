FROM continuumio/anaconda

RUN /opt/conda/bin/conda update conda -y --quiet && \
    /opt/conda/bin/conda install jupyter pandas scikit-learn numpy scipy psycopg2 sqlalchemy -y --quiet && \
    mkdir /opt/notebooks

CMD ["/opt/conda/bin/jupyter-notebook", "--notebook-dir=/opt/notebooks", "--ip='*'", "--port=8888", "--no-browser"]
