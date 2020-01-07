##
# Download Files
##
FROM ichbinbarbosa/php-w:72 AS dllcompile

# Promote powershell as default shell
#
SHELL ["powershell", "-Command", "$ErrorActionPreference = 'Stop';"]

ADD https://github.com/Microsoft/msphpsql/releases/download/v5.4.0-preview/Windows-7.2.zip /msphpsql.zip

RUN Expand-Archive -Path /msphpsql.zip -DestinationPath /msphpsql

# Promote powershell as default shell
#
RUN Add-Content /php/php.ini "extension=php_pdo_sqlsrv_72_nts"
RUN Add-Content /php/php.ini "extension=php_sqlsrv_72_nts"

##
# Build principal image
##
FROM ichbinbarbosa/php-w:72

COPY --from=dllcompile /php/php.ini /php/php.ini
COPY --from=dllcompile /msphpsql/Windows-7.2/x64/php_pdo_sqlsrv_72_nts.dll /php/ext
COPY --from=dllcompile /msphpsql/Windows-7.2/x64/php_sqlsrv_72_nts.dll /php/ext
