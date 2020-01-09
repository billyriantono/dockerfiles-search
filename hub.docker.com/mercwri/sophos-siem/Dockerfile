FROM python:3.7-alpine

WORKDIR /opt

ADD Sophos-Central-SIEM-Integration  /opt/Sophos-Central-SIEM-Integration

COPY entrypoint.sh /opt/Sophos-Central-SIEM-Integration/entrypoint.sh

ENTRYPOINT ["/opt/Sophos-Central-SIEM-Integration/entrypoint.sh"]
