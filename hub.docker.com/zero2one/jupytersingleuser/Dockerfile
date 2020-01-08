FROM jupyter/minimal-notebook:latest

EXPOSE 8888

USER root
RUN echo "dash dash/sh boolean false" | debconf-set-selections && \
    DEBIAN_FRONTEND=noninteractive dpkg-reconfigure dash && \
    apt-get update -y && \
    apt-get upgrade -y && \
    apt-get install -y --no-install-recommends libav-tools && \
    apt-get install -y htop fonts-ipafont fonts-ipaexfont && \
    apt-get clean -y && \
    rm -rf /var/lib/apt/lists/* && \
    wget -q https://raw.githubusercontent.com/jupyterhub/jupyterhub/0.6.1/scripts/jupyterhub-singleuser -O /usr/local/bin/jupyterhub-singleuser && \
    chmod 755 /usr/local/bin/jupyterhub-singleuser

ADD singleuser.sh /srv/singleuser/singleuser.sh

USER $NB_USER

ENV XDG_CACHE_HOME /home/$NB_USER/.cache/
RUN conda update --all -c defaults --yes && \
    conda config --set channel_priority false && \
    conda install -c defaults --yes ipywidgets pandas numexpr matplotlib scipy seaborn scikit-learn scikit-image sympy cython patsy statsmodels cloudpickle dill numba bokeh sqlalchemy hdf5 h5py && \
    conda install -c conda-forge jupyterlab tensorflow jupyter_contrib_nbextensions jupyter_nbextensions_configurator --yes && \
    conda install anaconda-nb-extensions -c anaconda-nb-extensions --yes && \
    conda remove --yes --force qt pyqt && \
    conda clean --all --yes && \
    jupyter nbextension enable --py widgetsnbextension --sys-prefix && \
    jupyter serverextension enable --py jupyterlab --sys-prefix && \
    jupyter nbextension enable autosavetime/main --user && \
    jupyter nbextension enable dragdrop/main --user && \
    jupyter nbextension enable toc2/main --user && \
    jupyter nbextension enable collapsible_headings/main --user && \
    jupyter nbextension enable codefolding/main --user && \
    pip --no-cache-dir install git+https://github.com/yuvipanda/nbresuse.git && \
    jupyter serverextension enable --py nbresuse && \
    jupyter nbextension install --py nbresuse --user && \
    jupyter nbextension enable nbresuse --user --py && \
    sh /srv/singleuser/singleuser.sh -h && \
    MPLBACKEND=Agg python -c "import matplotlib.pyplot" && \
    mkdir -p $HOME/.ipython/profile_default/startup
COPY mplimporthook.py $HOME/.ipython/profile_default/startup/
COPY scikit_learn_data /home/jovyan/scikit_learn_data
CMD ["sh", "/srv/singleuser/singleuser.sh"]
# フォントキャッシュ先に作っておく
# python -c "import matplotlib.pyplot"云々
# matplotlib inlineを常に入れる
# mplimporthook.py $HOME/.ipython/profile_default/startup/ 云々
