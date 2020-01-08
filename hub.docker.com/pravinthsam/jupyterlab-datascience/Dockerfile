FROM tensorflow/tensorflow:1.6.0-gpu-py3

# Install Jupyter Lab
RUN pip install jupyterlab==0.31.12 keras==2.1.5 seaborn==0.8.1 tqdm==4.19.7

# Start the jupyter lab
ENTRYPOINT jupyter lab --port=8888 --allow-root
