FROM pypy:3
MAINTAINER Giovanni De Gasperis @giodegas

RUN apt-get update && apt-get upgrade -y && apt-get -y install vim nano screen

WORKDIR /app

COPY requirements.txt ./
RUN pip install --no-cache-dir -r requirements.txt

COPY run.py /app/.

CMD [ "bash" ]
