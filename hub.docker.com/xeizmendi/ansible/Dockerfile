FROM python:2.7

ENV ANSIBLE_VERSION 2.2.0.0

RUN pip install --no-cache-dir ansible===$ANSIBLE_VERSION && apt-get update && apt-get install -y sshpass --no-install-recommends && rm -rf /var/lib/apt/lists/*

CMD ["ansible"]
