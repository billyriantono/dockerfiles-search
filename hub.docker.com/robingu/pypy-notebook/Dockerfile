FROM pypy:3.5-7

WORKDIR /app
ENV TZ=Asia/Beijing
#COPY sources.list /etc/apt/sources.list

#COPY pip.conf /root/.pip/pip.conf
COPY requirements.txt ./
RUN pip3 install --upgrade pip
RUN pip3 install --no-cache-dir -r requirements.txt

EXPOSE 8888/tcp
CMD [ "jupyter", "notebook", "--allow-root", "--ip=0.0.0.0", "--no-browser" ]