FROM eclipse/che-theia:plugin-id-nightly
RUN sudo mkdir /node_modules
RUN echo '"--*.modules-folder" "/node_modules"' > $HOME/.yarnrc
RUN sudo find /node_modules -exec sh -c "chgrp 0 {}; chmod g+rwX {}" \;
