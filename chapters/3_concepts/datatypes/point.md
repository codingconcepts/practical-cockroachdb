# Point

``` sql
CREATE TABLE "person" (
  "id" UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  "current_location" GEOMETRY NOT NULL
);
```

``` sql
INSERT INTO "person" ("current_location") VALUES (
   ST_SetSRID(ST_Makepoint(51.539188, -0.142500), 4326)
)
RETURNING "id";
```

``` sql
SELECT "id" FROM "person"
WHERE ST_Within(st_geomfromtext('SRID=4326;POINT(51.539188 -0.142500)'), st_geomfromtext('SRID=4326;POLYGON((51.570668 -0.134856, 51.520066 -0.066833, 51.521348 -0.195327, 51.570668 -0.134856))'));

SELECT "id" FROM "person"
WHERE ST_Within(st_geomfromtext('SRID=4326;POINT(51.539188 -0.142500)'), st_geomfromtext('SRID=4326;POLYGON((52.570668 -0.134856, 52.520066 -0.066833, 52.521348 -0.195327, 52.570668 -0.134856))'));
```

## Index

``` sql
CREATE INDEX "person_current_location" ON "person" USING GIST("current_location");
```