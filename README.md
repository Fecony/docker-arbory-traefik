# Docker Compose Arbory | Traefik

This is Docker Compose for Arbory projects (PHP + MySQL + NGINX) and Traefik.

## Usage

To get started, make sure you have [Docker installed](https://docs.docker.com/get-docker/) on your system, and then clone this repository.

## Setup

### **First add your Laravel project to the `src` folder.**

Create Docker network

```bash
docker network create traefik
```

Start Traefik

```bash
cd traefik
docker-composer up -d
```

Add environment data.

```bash
cd ../testapp
cp .env.example .env
nano .env
```

Add `init.sql` file to `data` folder. Which will create project database. Or import sql file later

## Run

```bash
docker-compose up -d
```

## Commands

- `docker-compose exec app bash` - to run bash in app container.
- `docker-compose exec mysql bash` - to access mysql. Then you can import/export database.

## TODO

- Need to understand traefik and dnsmasq more, to access multiple projects on different domains.
