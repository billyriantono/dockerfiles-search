FROM python
COPY . /src
RUN pip install -r src/requirements.txt
RUN pip install -U googlemaps
WORKDIR /src
CMD ["python", "test.py"]
