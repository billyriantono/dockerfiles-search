FROM jupyterhub/jupyterhub
MAINTAINER Denis OMeally <domeally@coh.org>
LABEL authors="domeally@coh.org" \
    description="Docker image containing all requirements for Jupyterhub with SlurmSpawner"

RUN pip install batchspawner
RUN pip install git+https://github.com/jupyterhub/wrapspawner
