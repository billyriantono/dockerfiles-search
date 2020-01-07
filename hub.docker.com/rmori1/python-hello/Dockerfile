FROM python:3
COPY server.py /
COPY requirements.txt /
RUN pip3 install aiohttp
CMD [ "python3", "-u", "server.py" ]
