FROM jupyter/datascience-notebook

# run as root to grant sudo access
# see https://hub.docker.com/r/jupyter/scipy-notebook/
USER root

# primary dependencies
RUN conda install numpy
RUN pip install deap update_checker tqdm stopit

# optional dependencies
## TPOT eXtreme Gradient Boosting
RUN conda install py-xgboost
## TPOT-MDR configuration
RUN pip install scikit-mdr skrebate

# install TPOT
RUN pip install tpot