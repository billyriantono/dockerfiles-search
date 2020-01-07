
from sjfloat/dev

user root
run curl -sL https://deb.nodesource.com/setup_4.x | bash -
run apt-get install -y nodejs
run npm install nodemon -g
run npm install bower -g

#
# https://docs.npmjs.com/getting-started/fixing-npm-permissions
#
# Step 03 of Getting Started - Repairing the damage already done by steps 01 and 02
#
run chown -R $USER /home/$USER/.npm

user $USER
cmd $SHELL -l
