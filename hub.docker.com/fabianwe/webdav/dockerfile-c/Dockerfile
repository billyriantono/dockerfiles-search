FROM python:3.6

EXPOSE 25

ENTRYPOINT ["python", "-u", "-m", "smtpd", "-n", "-c", "DebuggingServer", "0.0.0.0:25"]
