# Postgres

- Render creates backup of PostgreSQL database every 7 days by default
- backups can be downloaded from dashboard as sql or tar file

# Docker
- https://www.postgresql.org/docs/12/app-pgdump.html
- https://stackoverflow.com/questions/30171063/how-to-generate-a-postgresql-dump-from-a-docker-container

## Backup
- `sudo docker exec foodplanet_db pg_dump -U postgres -F p foodplanet_db -t food > backup.sql`

## Restore
- `cat backup_food_nutrient.sql | sudo docker exec -i foodplanet_db psql -U postgres`

# Questions
- remove VS Code syntax errors
- Create Render backup manually
- How to restore Render production db from sql dump?
- pg admin renaming
- tiger_data, tiger, topology
- limit dump file to public schema

### What are these errors when creating db from backup file
- it's about tiger, etc.

### Connect to Render database with pgadmin
- Right click on Servers in menu on left side: Create -> Server
- General>Name: "any-name"
- Connection>Host name/address: frankfurt-postgres.render.com
- Connection>Port: 5432
- Connection>Maintenance database: foodplanet_db
- Connection>Username: foodplanet
- Connection>Passwort: "your-password"

### Autorename INDEX, SEQUENCE, CONSTRAINT if table renamed
- no relation between table names and index/sequence/constraint names
- script could hit false positives

### Retrieve data from Render production db and insert it into Docker fp_test db
- add `\c fp_test`
- `cat backup_food_nutrient.sql | sudo docker exec -i foodplanet_db psql -U postgres`

### Database Cluster/Postgres Instance contains multiple databases

### What is a schema?
- namespace that contains named db objects (tables, indexes, data types,)
- db can contain multiple schemas
- each schema belongs to only one db
- two schemas can have different objects that share same name
- organise db objects into logical groups
- PostgreSQL default schema: `public`

### Information about pg_dump output file
- verbosity to ensure compatability
- COPY faster than INSERT