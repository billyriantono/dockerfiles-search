FROM python:3.8

COPY bashrc packages.txt requirements.txt /

RUN \
       mkdir -p /code \
    \
    && useradd user \
    && mkdir -p /home/user/.parallel \
    && chown user /home/user \
    \
    && cat /bashrc >>/home/user/.bashrc \
    && cat /bashrc >>/root/.bashrc \
    && chown user:user /home/user/.bashrc \
    && touch /home/user/.parallel/will-cite

RUN \
       apt-get update \
    && apt-get install -y --no-install-recommends $( cat /packages.txt )

RUN \
       pip3 install --upgrade pip setuptools \
    && pip3 install -r /requirements.txt

WORKDIR /code

CMD [ "python", "manage.py", "runserver", "0.0.0.0:8000" ]

USER user
