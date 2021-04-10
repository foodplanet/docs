# Development

### Create

```bash
sudo docker run --name foodplanet -p 6666:5432 -e POSTGRES_PASSWORD=1234 -d postgres
sudo docker run --name usda_local_pg_db -p 5560:5432 -e POSTGRES_PASSWORD=1234 -d postgres
```

### Execute script

```bash
cat foods.sql | sudo docker exec -i foodplanet psql -U postgres foodplanet
```

### Start

```bash
sudo docker start foodplanet
sudo docker start usda_local_pg_db
```

### Connect

```bash
sudo docker exec -it foodplanet psql -U postgres
sudo docker exec -it usda_local_pg_db psql -U postgres
```

### Backup

```bash
sudo docker exec foodplanet pg_dump -U postgres foodplanet -t '"Food"' -t '"Fact"' -t '"NutrientValue"' --data-only > foods.sql
cat foods.sql | sudo docker exec -i foodplanet psql -U postgres foodplanet
```

# Production

### Connect

```bash
PGPASSWORD=<password> psql -h frankfurt-postgres.render.com -U foodplanet foodplanet
```

### Execute script

```bash
PGPASSWORD=<password> psql -h frankfurt-postgres.render.com -U foodplanet foodplanet -f script.sql
```