---
{"dg-publish":true,"permalink":"/learn/monitoring-and-observability/grafana/basic-docker-grafana-and-postgres-setup-on-an-ec-2-instance/","noteIcon":""}
---

- Initialized an [[ec2\|ec2]] instance
- Installed [[docker\|docker]] in it
	- `sudo yum install -y docker`
	- `sudo service docker start`
	- Adjusted permissions so that it doesn't need sudo: `sudo usermod -a -G docker ec2-user`
- Installed [[learn/Monitoring and Observability/Grafana/Grafana\|Grafana]] using [[docker\|docker]] in it
	- `docker run -d -p 3010:3000 --name=grafana --volume grafana-storage:/var/lib/grafana grafana/grafana-enterprise`
- Installed [[Postgres\|Postgres]] using [[docker\|docker]] in it
	- `docker run -d -p 5432:5432 --name=postgres -e POSTGRES_PASSWORD=hehe -v postgres-data:/var/lib/postgresql/data postgres`
	- database: postgres
	- username: postgres
	- password: hehe