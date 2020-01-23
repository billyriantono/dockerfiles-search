FROM python:3.7.5-slim-buster
WORKDIR /usr/src/app
RUN echo 'requests' > requirements.txt
RUN echo 'flask' >> requirements.txt
RUN pip install --no-cache-dir -r requirements.txt
EXPOSE 8000
CMD [ "python"]