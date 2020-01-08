FROM python:3
ENV PYTHONUNBUFFERED 1
RUN mkdir /code
WORKDIR /code
RUN git clone https://github.com/mitsest/paging_api.git source && mv source/paging_api/* . && rm -rf source
RUN pip install -r Requirements
COPY . /code/
