ARG BASE_CONTAINER=jupyter/base-notebook:ff9357a77d78
# ARG BASE_CONTAINER=jupyter/all-spark-notebook:abdb27a6dfbb
FROM $BASE_CONTAINER

USER root

# Install all OS dependencies for fully functional notebook server
RUN apt-get update && apt-get install -yq --no-install-recommends \
  build-essential \
  git \
  inkscape \
  libsm6 \
  libxext-dev \
  libxrender1 \
  lmodern \
  netcat \
  pandoc \
  python-dev \
  texlive-fonts-extra \
  texlive-fonts-recommended \
  texlive-generic-recommended \
  texlive-latex-base \
  texlive-latex-extra \
  texlive-xetex \
  tzdata \
  unzip \
  ffmpeg \
  && rm -rf /var/lib/apt/lists/*


USER $NB_UID

COPY class_environment.yml /tmp/

  # Install Jupyter Notebook, Lab, and Hub
  # Generate a notebook server config
  # Cleanup temporary files
  # Correct permissions
  # Do all this in a single RUN command to avoid duplicating all of the
  # files across image layers when the permissions change
RUN conda install --quiet --yes \
  'notebook=5.7.8' \
  'jupyterhub=1.0.0' \
  'jupyterlab=0.35.5' && \
  conda clean --all -f -y && \
  jupyter labextension install @jupyterlab/hub-extension@^0.12.0 && \
  npm cache clean --force && \
  # jupyter notebook --generate-config && \
  # This is where I install the rest of the packages. The above are pulled out
  # so that I know what the jupyterhub and jupyterlab versions are.
  conda env update -n base --file /tmp/class_environment.yml  && \
  conda remove --quiet --yes --force qt pyqt && \
  conda clean --all -f -y && \
  # Activate ipywidgets extension in the environment that runs the notebook server
  jupyter nbextension enable --py widgetsnbextension --sys-prefix && \
  # Also activate ipywidgets extension for JupyterLab
  # Check this URL for most recent compatibilities
  # https://github.com/jupyter-widgets/ipywidgets/tree/master/packages/jupyterlab-manager
  jupyter labextension install @jupyter-widgets/jupyterlab-manager@^0.38.1 && \
  jupyter labextension install jupyterlab_bokeh@0.6.3 && \
  npm cache clean --force && \
  rm -rf $CONDA_DIR/share/jupyter/lab/staging && \
  rm -rf /home/$NB_USER/.cache/yarn && \
  rm -rf /home/$NB_USER/.node-gyp && \
  fix-permissions $CONDA_DIR && \
  fix-permissions /home/$NB_USER

USER root


# COPY class_linux_environment.yml /tmp/
# COPY class_environment.yml /tmp/
# RUN conda env update -n base -f /tmp/class_linux_environment.yml && \
#   conda clean -tipsy

RUN pip install nbgitpuller && \
  jupyter serverextension enable --py nbgitpuller --sys-prefix


# RUN n=0; max=300; while [ "$n" -le "$max" ]; do mkdir "/mnt/group$n"; n=`expr "$n" + 1`; done
# RUN mkdir /mnt/data /mnt/shared

COPY personal_start.sh /usr/local/bin/before-notebook.d/

USER $NB_UID

