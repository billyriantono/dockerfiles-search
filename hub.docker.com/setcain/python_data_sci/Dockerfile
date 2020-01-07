FROM python:3.7

LABEL maintainer='setcain'

WORKDIR /app

COPY . /app

RUN pip install -r requirements.txt

# make this port available out of this container
EXPOSE 8000

# run jupyter when container launches
CMD ["jupyter", "notebook", "--ip='0.0.0.0'", "--port=8000", "--no-browser", "--allow-root"]
