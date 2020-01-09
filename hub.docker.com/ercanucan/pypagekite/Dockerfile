FROM python:2.7

# Set the working directory to /pagekite
WORKDIR /pagekite

RUN curl -O https://pagekite.net/pk/pagekite.py
RUN chmod +x pagekite.py
RUN mv -f pagekite.py /usr/local/bin

EXPOSE 80 443

ENTRYPOINT ["python", "/usr/local/bin/pagekite.py", "--isfrontend"]
