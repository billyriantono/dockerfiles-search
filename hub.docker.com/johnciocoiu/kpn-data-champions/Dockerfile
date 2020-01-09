FROM jupyter/scipy-notebook:latest

ADD . /home/jovyan/work

WORKDIR /home/jovyan/work

# Expose the notebook port
EXPOSE 8888

# Start the notebook server
CMD jupyter notebook --no-browser --port 8888 --ip=*