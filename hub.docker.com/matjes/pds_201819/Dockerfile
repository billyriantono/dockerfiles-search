FROM tensorflow/tensorflow:latest-gpu-py3

# Install ML-Packages
RUN pip --no-cache-dir install \
  xgboost \
  catboost \
  lightgbm \
  gensim \
  seaborn \
  jupyter_contrib_nbextensions \
  jupyter_nbextensions_configurator

# Add Jupyter Extensions
RUN jupyter contrib nbextension install --user
RUN jupyter nbextensions_configurator enable --user

# Install Featuretools
RUN python -m pip install featuretools