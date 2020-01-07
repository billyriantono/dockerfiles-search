
FROM jupyter/minimal-notebook

USER root

USER $NB_UID

# Install Python 3 packages
RUN conda install --quiet --yes \
    'conda-forge::blas=*=openblas' \
    'bokeh=1.3*' \
    'cartopy' \
    'cx_oracle' \
    'cython=0.29*' \
    'dask=2.2.*' \
    'h5py=2.9*' \
    'hdf4' \
    'ffmpeg' \
    'jupyterlab=1.1.*' \
    'datashader' \
    'xarray' \
    'hdf5=1.10*' \
    'ipywidgets=7.5*' \
    'matplotlib-base=3.1.*' \
    'numba=0.45*' \
    'numexpr=2.6*' \
    'plotly=4.*' \
    'pandas=0.25*' \
    'scipy=1.3*' \
    'seaborn=0.9*' \
    'sqlalchemy=1.3*' \
    'statsmodels=0.10*' \
    'sympy=1.4*'

RUN pip install \
    autopep8 \
    black \
    cached-property \
    f90nml \
    ford \
    jupyterlab-code-formatter \
    pint \
    uncertainties
    
RUN conda clean --all -f -y && \
    # Activate ipywidgets extension in the environment that runs the notebook server
    jupyter nbextension enable --py widgetsnbextension --sys-prefix && \
    # Also activate ipywidgets extension for JupyterLab
    # Check this URL for most recent compatibilities
    # https://github.com/jupyter-widgets/ipywidgets/tree/master/packages/jupyterlab-manager
    jupyter labextension install @jupyter-widgets/jupyterlab-manager --no-build && \
    jupyter labextension install jupyterlab-plotly --no-build && \
    jupyter labextension install plotlywidget --no-build && \
    jupyter labextension install @ryantam626/jupyterlab_code_formatter --no-build && \
    jupyter labextension install jupyterlab_bokeh --no-build && \
    jupyter lab build --dev-build=False --log-level=0 && \
    npm cache clean --force && \
    rm -rf $CONDA_DIR/share/jupyter/lab/staging && \
    rm -rf /home/$NB_USER/.cache/yarn && \
    rm -rf /home/$NB_USER/.node-gyp && \
    fix-permissions $CONDA_DIR && \
    fix-permissions /home/$NB_USER

# Import matplotlib the first time to build the font cache.
ENV XDG_CACHE_HOME /home/$NB_USER/.cache/
RUN MPLBACKEND=Agg python -c "import matplotlib.pyplot" && \
    fix-permissions /home/$NB_USER

USER $NB_UID
