FROM mbaltrusitis/deb-base:wheezy

ENV LANG "C"

RUN git clone https://github.com/drzoidberg33/plexpy.git /opt/plexpy

EXPOSE 8181

CMD ["python", "/opt/plexpy/PlexPy.py --nolaunch --datadir=/configdata/plexpy/data"]
