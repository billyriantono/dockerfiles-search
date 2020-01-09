
FROM topiaruss/dicomtk

# where we mount hashes at runtime
RUN mkdir /root/.ssh

COPY requirements.txt /
RUN pip install -r requirements.txt

COPY deid.sh /

RUN mkdir /cleaned

COPY . /
