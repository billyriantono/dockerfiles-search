FROM jupyter/datascience-notebook

# Update conda first to fix IsADirectoryError
RUN conda install -n base conda && \
    conda install seaborn rpy2 geopandas && \
    conda install -c anaconda \
        networkx nltk pytables psycopg2 simplegeneric && \
    conda install -c conda-forge \
        altair geoplot proj4 ipyleaflet geojson \
        ipython-sql elasticsearch elasticsearch-dsl \
        neo4j-python-driver feather-format descartes && \
    conda install -c damianavila82 rise && \
    pip install nx_altair && \
    pip install z3-solver && \
    pip install geovoronoi && \
    pip install sqlalchemy geoalchemy2 && \
    jupyter labextension install @jupyterlab/vega3-extension && \
    jupyter labextension install jupyter-leaflet && \
    jupyter labextension install @jupyter-widgets/jupyterlab-manager

# Add the examples
USER jovyan
ADD examples /home/jovyan/examples
