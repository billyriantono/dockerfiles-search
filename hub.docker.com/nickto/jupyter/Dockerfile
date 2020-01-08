FROM nickto/python:latest

USER root

RUN pip install jupyterlab
EXPOSE 8888 
WORKDIR /app

CMD ["jupyter", "lab", "--ip=0.0.0.0", "--allow-root", "--no-browser"]

