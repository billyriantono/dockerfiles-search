FROM python:3.8.0-slim-buster
COPY ./app/ /app/
EXPOSE 9000
RUN pip3 install colorama pyopenssl requests tqdm unidecode Pillow BeautifulSoup4 urllib3 Flask pyusb pyqt5 google-api-python-client google-auth-oauthlib

RUN ["chmod", "+x", "/app/start.sh"]

CMD ["/app/start.sh"]
