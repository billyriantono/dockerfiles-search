FROM felipeb/repo:base-chromium73-python3.7-alpine

# copy files
WORKDIR /app
COPY browser/ .
COPY robots/ .
COPY queues.py .
COPY run.py .
COPY requirements.txt .

# install dependencies
RUN pip install -r requirements.txt

# run
# CMD [ "python3", "/app/run.py" ]
