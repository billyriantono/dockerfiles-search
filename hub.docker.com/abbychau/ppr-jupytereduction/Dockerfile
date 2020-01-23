FROM jupyter/minimal-notebook

RUN conda install --quiet --yes faiss-cpu -c pytorch && \
conda install --quiet --yes gensim cmake gunicorn scikit-learn scipy numpy connexion flask && \
pip install git+https://github.com/DmitryUlyanov/Multicore-TSNE.git

COPY . /app

WORKDIR /app

CMD ["gunicorn", "--workers=4","--timeout=3600", "-b 0.0.0.0:5000","wsgi:app"]

EXPOSE 5000