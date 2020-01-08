# Copyright (c) Niels Borie.

FROM nielsborie/ml-docker

LABEL maintainer="s4ragent"

USER root

# --- Conda feather-format
RUN conda install -c conda-forge --quiet --yes \
    'feather-format' && \
    conda clean -tipsy && \
    fix-permissions $CONDA_DIR && \
    fix-permissions /home/$NB_USER

#RUN $CONDA_DIR/bin/python -m pip install --upgrade mpld3
RUN $CONDA_DIR/bin/python -m pip install kaggle \
					 flake8 \
					 optuna
# clean up pip cache
RUN rm -rf /root/.cache/pip/*
