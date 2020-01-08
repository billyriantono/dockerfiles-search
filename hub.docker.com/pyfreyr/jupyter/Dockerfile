FROM pyfreyr/python:3.7-bionic

RUN pip --no-cache-dir install \
        ipykernel \
        jupyter \
        && \
    python -m ipykernel.kernelspec

COPY jupyter_notebook_config.py /root/.jupyter/

COPY run_jupyter.sh /

WORKDIR /notebooks

EXPOSE 8888

VOLUME ["/notebooks"]

CMD ["/run_jupyter.sh", "--allow-root"]
