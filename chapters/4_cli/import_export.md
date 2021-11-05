``` sql
CREATE DATABASE import_export;
USE DATABASE import_export;

CREATE TABLE ex (
  name TEXT NOT NULL
);

INSERT INTO ex (name) VALUES ('A');
INSERT INTO ex (name) VALUES ('B');
INSERT INTO ex (name) VALUES ('C');

EXPORT INTO CSV 'https://2498-90-251-250-245.ngrok.io'
FROM TABLE ex;

EXPORT INTO CSV 'https://2498-90-251-250-245.ngrok.io'
WITH compression = 'gzip'
FROM TABLE ex;
```

``` sql
IMPORT TABLE im (
    name TEXT NOT NULL
  ) CSV DATA ('https://2498-90-251-250-245.ngrok.io/export16b3d02f10e76ee80000000000000001-n707164865270644737.0.csv');

IMPORT TABLE im (
    name TEXT NOT NULL
  ) CSV DATA ('https://2498-90-251-250-245.ngrok.io/export16b3d04909899e900000000000000001-n707165230783266817.0.csv.gz');
```

``` SQL
BACKUP DATABASE import_export INTO 'https://2498-90-251-250-245.ngrok.io'
AS OF SYSTEM TIME '-10s';
```