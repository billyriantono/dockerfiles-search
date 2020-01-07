FROM gcr.io/kubeflow-images-public/tensorflow-1.12.0-notebook-cpu:v0.4.0

RUN pip3 install --upgrade --no-cache-dir \
                 numpy==1.16.0 \
                 pandas==0.24.0 \
                 dask==1.1.1 \
                 dask-kubernetes==0.7.0 \
                 dask-ml==0.11.0 \
                 pyarrow==0.12.0 \
                 s3fs==0.2.0 \
                 bokeh==1.0.4 \
                 seaborn \
                 matplotlib

RUN source activate py2 && jupyter labextension install dask-labextension
