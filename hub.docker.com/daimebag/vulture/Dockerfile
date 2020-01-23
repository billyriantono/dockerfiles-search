FROM python:latest

RUN pip install vulture
RUN mkdir /app

RUN useradd vulture
USER vulture
WORKDIR /app

ENTRYPOINT ["vulture"]
CMD ["--sort-by-sise"]