# Odoo Community Edition


### [Odoo v15 Custom Docker Image Build Repository](https://github.com/<insert-pep-container-registry-url>)

Customised Odoo ce with Open HRMS and a Full accounting Kit available for install, Python Pandas preinstalled for use with HRMS.

*Before installing third party modules, please see their relative dependency modules which must be installed first.*

---

# Requirements
- Docker
- Docker Compose


# How to use the repo and odoo docker image

Adjust the docker compose file and odoo.conf, as well as extract any third party apps to the addons [folder](/Odoo-v15/addons/readme.md), to suit your project needs.

Navigate to the docker compose yaml file directory and run:

```
docker compose up -d
```
This will pull the image from the github container registry and run the image with the specified config



## Login to your respective container registry

```
docker login <registry url>ghcr.io/phylogenyexplorerproject/Odoo
```

## Change directory into the Dockerfile location

```
cd DockerBuild/15.0/
```

## Build the image from the Dockerfile

```
docker build -t ghcr.io/phylogenyexplorerproject/odoo:latest .
```

### where -t is to tag the image, default is latest or main depending on container registry.

### the period at the end of the line is to specify that the Dockerfile be built from its current path.

## Build the image with a different tag

```
docker build -t ghcr.io/phylogenyexplorerproject/odoo-pep:dev .

docker build -t ghcr.io/phylogenyexplorerproject/odoo-pep:staging .

docker build -t ghcr.io/phylogenyexplorerproject/odoo-pep:15.0 .
```

#### and so on

## Finally push your changes to the registry

```
docker push ghcr.io/phylogenyexplorerproject/odoo
```

### How to scaffold a new app using docker

#### Enter the container

```
docker exec -u root -it <containerID> /bin/bash
```

#### Inside the container, run

```
/usr/bin/odoo scaffold <yourappname> /mnt/extra-addons
```

##### If you have used this repo to create an app then your newly cretaed app will appear in the project folders under odoo/addons. This external path has been mapped to /mnt/extra-addons inside the container.

## Now change the file permissions to allow editing

```
sudo chown -R $USER:$USER <yourappname>
```



# Post install
; list_db = False in odoo.conf
this disables the database selector/manager on the public facing website


# How to update

Make sure your Dockerfile, entrypoint.sh, odoo.conf and wait-for-psql.py files are up to date with the latest (official Odoo docker repo)[https://github.com/odoo/docker]

## Third party apps like Open HRMS require python pandas:

### Include in Dockerfile

```
    python3-pandas \
```

#### Note on filestore path
By default Odoo uses /var/lib/odoo to store data, for this project the path has been set to /var/www/vhosts/phylogenyexplorerproject.org/odoo.phylogenyexplorerproject.org/ in odoo.conf


# [Join Clickonrefresh's Odoo Discord Community](https://discord.gg/46kKJ5VeHt)
# [The Phylogeny Explorer Project on Discord]()
