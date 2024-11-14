# Omicsdatascience Website


## Requirements

Docker volumes to be used in the `docker-compose.yml` must be created:

```
docker volume create --name=omicsdatascience_site_wordpress
docker volume create --name=omicsdatascience_site_db
```

## Steps to run Wordpress locally

**IMPORTANT:** read the docker-compose_local.yml file and comment/uncomment the corresponding lines to use the correct image.

1. Clone the repository
1. Run Docker compose with the `docker-compose_local.yml` file `docker-compose -f docker-compose_local.yml up -d`
1. Once you have all the changes you need, make a Duplicator dump.


## Steps to migrate the site to a new server

The following steps are for recovering a backup of a site on any server.

1. Create a package using the Duplicator plugin. (You can use [this backup]() functional from production)
1. Download the `installer.php` files and the `.zip` file of the Duplicator package inside the `website` folder.
1. Start an instance with our image `docker compose up -d`
1. Install package with Duplicator by accessing the URL where the Docker container was launched with the suffix `/installer.php`. E.g.: `127.0.0.1:8080/installer.php` and following the instructions.
1. Use Better Search and Replace to change everything that is `http://[IP:VPS port]` to `https://omicsdatascience.org`
1. Change the `WP_DEBUG` variable to `false` to put the site into production.
