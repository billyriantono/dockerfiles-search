# Created Date: 2018-01-22
# Updated Date: 2018-01-29
FROM debian
RUN ["apt-get", "update"]
RUN ["apt-get", "install", "python", "python-pip", "python3", "python3-pip", "-y"]
RUN ["python", "-m", "pip", "install", "--upgrade", "pip"]
RUN ["python", "-m", "pip", "install", "jupyter"]
RUN ["python3", "-m", "pip", "install", "--upgrade", "pip"]
RUN ["python3", "-m", "pip", "install", "jupyter"]
LABEL version="0.0.3" maintainer="Daye Lee<tosony@163.com>"
WORKDIR /root/
ENTRYPOINT ["jupyter", "notebook", "--no-browser", "--ip=0.0.0.0", "--allow-root"]
CMD ["--NotebookApp.password='sha1:bb9ea858e58e:0c502a42c7e476af2eff7fb60c7273f1ce09acdb'"]
EXPOSE 8888
