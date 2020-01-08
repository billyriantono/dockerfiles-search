FROM jupyter/datascience-notebook:latest
MAINTAINER geotaru

RUN pip install keras \
tensorflow \
numpy \
scikit-learn \
imbalanced-learn \
xgboost \
lightgbm \
pandas \
scipy \
seaborn \
matplotlib \
plotly \
jupyter \ 
tqdm \
cython \
jupyter_contrib_nbextensions \
pydot \
graphviz \
pydot3 \
pydot-ng \
folium

RUN conda update --all
RUN conda install -c damianavila82 \
rise

RUN jupyter contrib nbextension install --user && \
mkdir -p $(jupyter --data-dir)/nbextensions && \
cd $(jupyter --data-dir)/nbextensions && \
git clone https://github.com/lambdalisue/jupyter-vim-binding vim_binding &&  \
jupyter nbextension enable vim_binding/vim_binding && \
jupyter-nbextension install rise --py --sys-prefix && \
jupyter-nbextension enable rise --py --sys-prefix && \
jupyter nbextension enable --py widgetsnbextension --sys-prefix
