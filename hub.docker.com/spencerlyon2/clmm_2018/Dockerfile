FROM jupyter/scipy-notebook:27ba57364579

RUN pip install git+https://github.com/EconForge/interpolation.py.git && \
    pip install git+https://github.com/naught101/sobol_seq.git

CMD ["/opt/conda/bin/python", "/var/programfiles/NewKeynesian/python/main.py", "table"]
