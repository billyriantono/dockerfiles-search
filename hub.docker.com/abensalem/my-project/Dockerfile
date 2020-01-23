FROM python:3.6-alpine

RUN pip install mkdocs


RUN mkdir /documents
RUN mkdir /site
COPY . /documents/
WORKDIR /documents
RUN ls -l

#RUN mkdocs build
CMD ["mkdocs", "serve", "-a", "0.0.0.0:8000"]

EXPOSE 8000
