FROM jupyter/base-notebook:cd158647fb94
# https://hub.docker.com/layers/jupyter/base-notebook/cd158647fb94/images/sha256-c9df73049562ac22bfa572e6ee7a37c55b7608d33fa0330020f6b247d28570e6
# 12/9/2019 at 1:53 pm

# Bug in notebook 6.0.0 with custom content managers
# https://github.com/jupyter/notebook/pull/4891
RUN conda install -y -q --freeze-installed -c ome omero-py 'notebook>=6.0.2'

RUN python3 -mpip install fs-omero-pyfs jupyter-pyfilesystem

# Don't ignore configuration errors
ENV TRAITLETS_APPLICATION_RAISE_CONFIG_FILE_ERROR true

RUN mkdir -p $HOME/.jupyter/jupyter_notebook_config.d
RUN /bin/echo -e 'from glob import glob\nfor f in glob(".jupyter/jupyter_notebook_config.d/*py"): exec(open(f).read())' >> \
    $HOME/.jupyter/jupyter_notebook_config.py

ADD jupyter_notebook_config.py $HOME/.jupyter/jupyter_notebook_config.d/contentsmanager.py
