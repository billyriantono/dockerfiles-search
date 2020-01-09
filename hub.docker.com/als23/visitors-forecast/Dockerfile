FROM jupyter/scipy-notebook
RUN pip install pystan
COPY . /app
WORKDIR /app
RUN pip install -r requirements.txt
CMD python run.py
