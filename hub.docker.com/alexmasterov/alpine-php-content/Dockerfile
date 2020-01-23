FROM jupyter/scipy-notebook

USER root

USER $NB_USER 

RUN pip install git+https://github.com/Theano/Theano.git
COPY .theanorc "$HOME"/.theanorc 
RUN pip install git+https://github.com/pymc-devs/pymc3

RUN pip install pystan tqdm

RUN pip install dash dash-renderer dash-html-components dash-core-components
RUN pip install plotly

RUN conda install --quiet --yes basemap  pytables

RUN conda install -c conda-forge python-graphviz

# Import matplotlib the first time to build the font cache.
RUN python -c "import matplotlib.pyplot"
VOLUME ["/home/jovyan"]
