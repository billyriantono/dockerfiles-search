FROM jupyter/datascience-notebook
COPY req.txt /home/jovyan/
RUN pip install -r /home/jovyan/req.txt
COPY dl_nltk_punkt.py /home/jovyan/
RUN python /home/jovyan/dl_nltk_punkt.py
