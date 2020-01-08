FROM jupyter/datascience-notebook:749017d878d6

RUN pip3 install xlrd
RUN pip3 install xlwt
RUN pip3 install openpyxl
RUN pip3 install oauth2client
RUN pip3 install google-api-python-client
RUN pip3 install bs4
RUN pip3 install gmaps
RUN pip3 install folium
RUN jupyter nbextension enable --py --sys-prefix widgetsnbextension
RUN jupyter nbextension enable --py gmaps
RUN HDF5_DIR=/opt/conda/pkgs/hdf5-1.8.17-3 pip3 install tables
RUN conda install mkl-rt