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

## Run and Stop Containers

```bash
# To start containers
docker-compose up -d

# To stop them
docker-compose down
```

Now open `testapp.test` in your browser and you should see your application running!

- **NOTICE** - If it is not working for you, look at [Custom domain](#custom-domain-dev-test-etc) section to setup `dnsmasq`

## Commands

- `docker-compose exec app bash` - to run bash in app container.
- `docker-compose exec mysql bash` - to access mysql. Then you can import/export database.

## Custom domain (`.dev`, `.test`, etc...)

Possible fix for macOS DNS settings [here](https://superuser.com/questions/680005/in-os-x-how-can-i-prepend-127-0-0-1-to-the-list-of-dns-servers-obtained-through)

```bash
# Install dnsmasq
brew install dnsmasq

# MacOS fix
sudo mkdir /etc/resolver/
sudo sh -c 'echo nameserver 127.0.0.1 > /etc/resolver/DOMAIN_NAME'

# Open `dnsmasq` config file and add line:
# "conf-file=/Users/your_user_name/.dnsmasq/dnsmasq.conf"
nano /usr/local/etc/dnsmasq.conf

# Open /Users/your_user_name/.dnsmasq/dnsmasq.conf file
nano /Users/your_user_name/.dnsmasq/dnsmasq.conf

# add this lines
#
# address=/domain/127.0.0.1
# listen-address=127.0.0.1
#
# Where "domain" is domain you want to access your app

# Start dnsmasq
brew services start dnsmasq
```

Now you can access `testapp.domain` to access your project and start coding!
