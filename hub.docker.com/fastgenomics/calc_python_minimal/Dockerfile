FROM fastgenomics/scanpy:1.3.1-p36-v3

RUN pip3 install --no-cache-dir fastgenomics==2.0.5

COPY manifest.json LICENSE LICENSE-THIRD-PARTY /app/

COPY my_app /app/my_app
CMD python3 /app/my_app
