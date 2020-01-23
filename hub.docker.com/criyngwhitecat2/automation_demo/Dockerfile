FROM python:2.7-slim
WORKDIR /
COPY index.html index.py /
RUN pip install Flask 
EXPOSE 80
CMD ["python","index.py"]
