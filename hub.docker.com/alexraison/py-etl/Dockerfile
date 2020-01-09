FROM python:3

WORKDIR /app

COPY requirements.txt ./
RUN pip install --no-cache-dir -r requirements.txt

COPY . .
RUN mkdir /app/input_files/
RUN mkdir /app/output/


CMD [ "python", "-u", "./watch_directory.py" ]
