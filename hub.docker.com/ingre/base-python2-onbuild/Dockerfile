FROM ingre/base-python2

RUN mkdir -p /app
WORKDIR /app

ONBUILD COPY requirements.txt /app/
ONBUILD RUN pip install -r requirements.txt --trusted-host tcx999thi.pypi.ingre.pl --src /tmp/src

ONBUILD COPY . /app
