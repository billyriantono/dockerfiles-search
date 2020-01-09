FROM python:2-onbuild
RUN pip install qrcode
RUN pip install lxml
RUN pip install requests_toolbelt
RUN pip install coloredlogs
RUN pip install pyOpenSSL
RUN pip install ndg-httpsclient
RUN pip install pyasn1
RUN pip install itchat
CMD ["import","itchat"]
CMD ["import","itchat.pkl"]
CMD [ "python", "./wechat-robot.py" ]
