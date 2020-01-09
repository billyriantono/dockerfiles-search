ARG BASE_CONTAINER=jupyter/minimal-notebook
FROM $BASE_CONTAINER
LABEL author="anosillus"

USER $NB_UID
# Don't use pip in root

RUN jupyter labextension install @ryantam626/jupyterlab_code_formatter --no-build && \
    # Code Formatter https://github.com/ryantam626/jupyterlab_code_formatter
    conda install -c conda-forge black && \
    conda install -c conda-forge jupyterlab_code_formatter && \
    jupyter serverextension enable --py jupyterlab_code_formatter && \
    # Git-Sidebar https://github.com/jupyterlab/jupyterlab-git
    pip install --upgrade jupyterlab-git && \
    # Latex https://github.com/jupyterlab/jupyterlab-latex
    pip install jupyterlab_latex && \
    jupyter labextension install @jupyterlab/latex --no-build && \
    jupyter serverextension enable --sys-prefix jupyterlab_latex && \
    # Contents Table https://github.com/jupyterlab/jupyterlab-toc
    jupyter labextension install @jupyterlab/toc --no-build && \
    # Template Reader https://github.com/jpinzonc/jupyterlab_templates
    pip install jupyterlab_templates && \
    jupyter labextension install jupyterlab_templates --no-build && \
    jupyter serverextension enable --py jupyterlab_templates && \
    # jupyter serverextension enable --py jupyterlab_templates
    # add following into jupyter_notebook_config.py
    # c.JupyterLabTemplates.template_dirs = ['list', 'of', 'template', 'directories']
    # c.JupyterLabTemplates.include_default = True
    # Diff tool https://nbdime.readthedocs.io/en/latest/extensions.html
    pip install nbdime && \
    jupyter labextension install nbdime-jupyterlab --no-build && \

    # Spellchecker
    # https://github.com/ijmbarr/jupyterlab_spellchecker
    jupyter labextension install @ijmbarr/jupyterlab_spellchecker && \
    # sql
    pip install jupyterlab_sql && \
    conda install psycopg2 && \
    conda clean --all -f -y && \
    jupyter serverextension enable jupyterlab_sql --py --sys-prefix && \
    # widgetnbextension  https://github.com/jupyter-widgets/ipywidgets/tree/master/packages/jupyterlab-manager
    # jupyter nbextension enable --py widgetsnbextension --sys-prefix && \
    conda install ipywidgets && \
    jupyter labextension install @jupyter-widgets/jupyterlab-manager@^1.0.1 --no-build && \
    jupyter labextension install jupyterlab_bokeh@1.0.0 --no-build && \
    # build
    jupyter lab build --dev-build=False && \
    jupyter lab build && \
        jupyter lab clean && \
        jlpm cache clean && \
        npm cache clean --force && \
        rm -rf $HOME/.node-gyp && \
        rm -rf $HOME/.local && \
    fix-permissions $CONDA_DIR $HOME
