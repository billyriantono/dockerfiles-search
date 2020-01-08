FROM jupyter/base-notebook:latest

RUN conda install --yes --no-pin \
  numpy \
  pandas \
  geopandas \
  scikit-learn \
  scikit-image \ 
  xarray \
  statsmodels \
  rasterio \
  rasterstats \
  matplotlib \ 
  seaborn 

RUN conda install --yes --no-pin -c conda-forge \
  pingouin


