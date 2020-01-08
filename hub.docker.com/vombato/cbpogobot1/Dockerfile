FROM python:3

ADD app.py /

COPY Requirements.txt ./

RUN pip install --no-cache-dir -r Requirements.txt

COPY . .

CMD [ "python3", "app.py" ] 
