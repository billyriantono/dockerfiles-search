FROM python:3.7.4

WORKDIR /app

COPY ./gaussian_n_b.py /app/gaussian_n_b.py
COPY ./requirements.txt /app/requirements.txt
RUN pip3 install --no-cache-dir -r /app/requirements.txt

ENTRYPOINT [ "/bin/bash" ]
