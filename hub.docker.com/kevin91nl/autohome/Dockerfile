FROM python:3.5
RUN pip install "torch>=1.0.0,<2.0.0"
RUN pip install "pandas==0.24.2"
RUN pip install "matplotlib==3.0.3"
COPY requirements-dev.txt /requirements-dev.txt
RUN pip install -r /requirements-dev.txt
COPY requirements.txt /requirements.txt
RUN pip install -r /requirements.txt
RUN python -m nltk.downloader punkt stopwords
COPY . /app/
WORKDIR /app/
ENV PYTHONPATH "${PYTHONPATH}:/app"
EXPOSE 8888