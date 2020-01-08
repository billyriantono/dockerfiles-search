# ref: https://github.com/jupyterhub/zero-to-jupyterhub-k8s/issues/994
FROM jupyter/datascience-notebook:7f1482f5a136

# GPU powered ML
# ----------------------------------------
RUN conda install --yes --quiet -c conda-forge \
    tensorflow-gpu \
    cudatoolkit=9.0 && \
    conda clean -tipsy && \
    fix-permissions $CONDA_DIR && \
    fix-permissions /home/$NB_USER

# Allow drivers installed by the nvidia-driver-installer to be located
ENV LD_LIBRARY_PATH=${LD_LIBRARY_PATH}:/usr/local/nvidia/lib64
# Also, utilities like `nvidia-smi` are installed here
ENV PATH=${PATH}:/usr/local/nvidia/bin
