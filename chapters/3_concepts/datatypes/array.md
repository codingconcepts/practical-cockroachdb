# Array

## Create a table

``` sql
CREATE TABLE "person" (
  "id" UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  "pets" STRING[] NULL
);
```

``` sql
INSERT INTO "person" ("pets") VALUES (
  ARRAY['Molly', 'Lyla']
)
RETURNING "id";
```

``` sql
UPDATE "person"
SET "pets" = array_append("pets", 'Smedley')
WHERE "id" = 'af6118bd-f16b-444a-b35e-35ccc76b8bba';

UPDATE "person"
SET "pets" = array_remove("pets", 'Smedley')
WHERE "id" = 'af6118bd-f16b-444a-b35e-35ccc76b8bba';
```

``` sql
SELECT "pets" FROM "person"
WHERE "id" = 'af6118bd-f16b-444a-b35e-35ccc76b8bba';

SELECT "id" FROM "person"
WHERE "pets" @> ARRAY['Molly'];

SELECT "id" FROM "person"
WHERE ARRAY['Molly'] <@ "pets";
```

## Indexing

``` sql
explain select * from person where pets @> ARRAY['Molly'];
```

```
  distribution: full
  vectorized: true

  • filter
  │ estimated row count: 0
  │ filter: pets @> ARRAY['Molly']
  │
  └── • scan
        estimated row count: 1 (100% of the table; stats collected 3 hours ago)
        table: person@primary
        spans: FULL SCAN
(11 rows)
```

``` sql
CREATE INVERTED INDEX person_pets ON person (pets);
```

```
distribution: local
  vectorized: true

  • index join
  │ estimated row count: 0
  │ table: person@primary
  │
  └── • scan
        estimated row count: 0 (11% of the table; stats collected 3 hours ago)
        table: person@person_pets
        spans: 1 span
(11 rows)
```