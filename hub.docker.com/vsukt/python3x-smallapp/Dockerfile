FROM busybox:latest
RUN wget -c https://github.com/pts/staticpython/raw/master/release/python3.2-static -O /bin/python3 && chmod a+x /bin/python3
COPY app.py /app.py
CMD ["/bin/python3", "/app.py"]
