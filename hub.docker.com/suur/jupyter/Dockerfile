FROM continuumio/anaconda3:latest

# https://github.com/ContinuumIO/anaconda-issues/issues/9601#issuecomment-397340727
RUN /opt/conda/bin/conda install -c defaults libprotobuf protobuf -y --quiet \
    && /opt/conda/bin/conda clean --all --quiet
RUN /opt/conda/bin/conda install -c conda-forge opencv tensorflow python-levenshtein -y --quiet \
    && /opt/conda/bin/conda clean --all --quiet
RUN /opt/conda/bin/conda install -c anaconda psycopg2 boto3 -y --quiet \
    && /opt/conda/bin/conda clean --all --quiet
RUN /opt/conda/bin/conda install jupyter -y --quiet \
    && /opt/conda/bin/conda clean --all --quiet && mkdir /opt/notebooks

EXPOSE 8888

CMD /opt/conda/bin/jupyter notebook --allow-root --notebook-dir=/opt/notebooks --ip='*' --port=8888 --no-browser
