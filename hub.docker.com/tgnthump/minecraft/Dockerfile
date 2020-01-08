FROM itzg/minecraft-server:latest
LABEL org.freenas.interactive="false" 		\
      org.freenas.version="Latest (Auto Update)"		\
      org.freenas.upgradeable="false"		\
      org.freenas.expose-ports-at-host="true"	\
      org.freenas.autostart="true"		\
      # org.freenas.capabilities-add="NET_BROADCAST" \
      # org.freenas.web-ui-protocol="http"	\
      # org.freenas.web-ui-port=32400		\
      # org.freenas.web-ui-path="web"		\
      org.freenas.port-mappings="25565:25565/tcp"			\
      org.freenas.volumes="[					\
          {							\
              \"name\": \"/data\",				\
              \"descr\": \"Data\"		\
          },							\
          {							\
              \"name\": \"/transcode\",				\
              \"descr\": \"Video transcode directory\"		\
          },							\
          {							\
              \"name\": \"/data\",				\
              \"descr\": \"Media volume\"			\
          }							\
      ]"							\
      org.freenas.settings="[ 					\
          {							\
              \"env\": \"EULA\",					\
              \"descr\": \"Accept the Minecraft EULA\",		\
              \"optional\": true				\
          },\
          {							\
              \"env\": \"UID\",					\
              \"descr\": \"UID\",		\
              \"optional\": true				\
          },\
          {							\
              \"env\": \"GID\",					\
              \"descr\": \"GID\",		\
              \"optional\": true				\
          },\
          {							\
              \"env\": \"VERSION\",					\
              \"descr\": \"Version\",		\
              \"optional\": true				\
          },\
          {							\
              \"env\": \"TYPE\",					\
              \"descr\": \"Type\",		\
              \"optional\": true				\
          },\
          {							\
              \"env\": \"FORGEVERSION\",					\
              \"descr\": \"Forge Version\",		\
              \"optional\": true				\
          },\
          {							\
              \"env\": \"FORGE_INSTALLER\",					\
              \"descr\": \"FORGE_INSTALLER\",		\
              \"optional\": true				\
          },\
          {							\
              \"env\": \"FORGE_INSTALLER_URL\",					\
              \"descr\": \"FORGE_INSTALLER_URL\",		\
              \"optional\": true				\
          },\
          {							\
              \"env\": \"FTB_SERVER_MOD\",					\
              \"descr\": \"FTB_SERVER_MOD\",		\
              \"optional\": true				\
          },\
          {							\
              \"env\": \"MIN_RAM\",					\
              \"descr\": \"MIN_RAM\",		\
              \"optional\": true				\
          },\
          {							\
              \"env\": \"MAX_RAM\",					\
              \"descr\": \"MAX_RAM\",		\
              \"optional\": true				\
          }\
      ]"
