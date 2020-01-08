FROM python:3.6

RUN useradd -m wow

USER wow
WORKDIR /home/wow

RUN git clone https://github.com/morihisa/WOWHoneypot.git /home/wow/WOWHoneypot

WORKDIR /home/wow/WOWHoneypot

ENTRYPOINT ["python3", "-u", "wowhoneypot.py"]
