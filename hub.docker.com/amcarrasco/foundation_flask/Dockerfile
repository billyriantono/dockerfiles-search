FROM continuumio/miniconda3:latest

LABEL maintainer="Alec Carrasco"

COPY src /src/
COPY requirements.txt /src/requirements.txt
WORKDIR /src/
RUN conda install -c anaconda lxml -y
RUN pip install -r requirements.txt

EXPOSE 3838

ENTRYPOINT ["python", "/src/app.py"]