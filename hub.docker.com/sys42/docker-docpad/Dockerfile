FROM sys42/docker-nodejs:1.0.0
MAINTAINER Tom Nussbaumer <thomas.nussbaumer@gmx.net>
RUN sudo -iu app bash -c ". ~/.nvm/nvm.sh npm install -g npm && npm install -g docpad@6.78" && \
echo 'name: "MAC ec8fdeb1c389df0b478069f8a3d5c3ccf3cb1428"' > /home/app/.docpad.cson && \
echo 'email: null' >> /home/app/.docpad.cson && \
echo 'username: "ec8fdeb1c389df0b478069f8a3d5c3ccf3cb1428"' >> /home/app/.docpad.cson && \
echo 'subscribed: false' >> /home/app/.docpad.cson && \
echo 'subscribeTryAgain: null' >> /home/app/.docpad.cson && \
echo 'tos: true' >> /home/app/.docpad.cson && \
echo -n 'identified: true' >> /home/app/.docpad.cson && \
chown app:app /home/app/.docpad.cson
