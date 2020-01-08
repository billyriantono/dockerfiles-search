FROM php:7.3-alpine

ADD "https://raw.githubusercontent.com/jdorn/sql-formatter/master/lib/SqlFormatter.php" "/opt/SqlFormatter.php"

COPY "entry.php" "/opt/entry.php"

ENTRYPOINT ["php", "/opt/entry.php"]
