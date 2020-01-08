FROM python:3.6

RUN mkdir -p /data
WORKDIR /data


RUN ls

# ADD entrypoint.sh /entrypoint
# RUN chmod +x  /entrypoint
# CMD ["gunicorn", "-b", "0.0.0.0:8000", "app:app"]
RUN pip install gunicorn

ENTRYPOINT ["/data/entrypoint"]