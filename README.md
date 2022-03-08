# Odoo Community Edition


### [Odoo v15 Custom Docker Image Build Repository](https://github.com/<insert-pep-container-registry-url>)

Customised Odoo ce with Open HRMS and a Full accounting Kit available for install, Python Pandas preinstalled for use with HRMS.

Before installing third party modules, please see their relative dependency modules which must be installed first.

---

# Requirements
- Docker
- Docker Compose



# How to update

Make sure your Dockerfile, entrypoint.sh, odoo.conf and wait-for-psql.py files are up to date with the latest (official Odoo docker repo)[https://github.com/odoo/docker]

## Third party apps like Open HRMS require python pandas:

### Include in Dockerfile

```
    python3-pandas \
```

#### Note on filestore path
By default Odoo uses /var/lib/odoo to store data, for this project the path has been set to /var/www/vhosts/phylogenyexplorerproject.org/odoo.phylogenyexplorerproject.org/ in odoo.conf

# How to use this repo image

## Login to your respective container registry

`docker login <registry url>`

## Change directory into the Dockerfile location

`cd DockerBuild/15.0/`

## Build the image from the Dockerfile

`docker build -t ghcr.io/phylogenyexplorerproject/odoo-pep .`

### where -t is to tag the image, default is latest or main depending on container registry.

### the period at the end of the line is to specify that the Dockerfile be built from its current path.

## Build the image with a different tag

`docker build -t ghcr.io/phylogenyexplorerproject/odoo-pep:dev .`
`docker build -t ghcr.io/phylogenyexplorerproject/odoo-pep:staging .`
`docker build -t ghcr.io/phylogenyexplorerproject/odoo-pep:15.0 .`

#### and so on

## Finally push your changes to the registry

`docker push ghcr.io/phylogenyexplorerproject/odoo-pep`
fails with bad credential setup

# How to scaffold a new app using docker

## Enter the container

`docker exec -u root -it <containerID> /bin/bash`

## Inside the container, run

`/usr/bin/odoo scaffold <yourappname> /mnt/extra-addons`

### If you have used this repo to create an app then your newly cretaed app will appear in the project folders under odoo/addons. This external path has been mapped to /mnt/extra-addons inside the container.

## Now change the file permissions to allow editing

`sudo chown -R $USER:$USER <yourappname>` -->

# [Join My Odoo Discord Community](https://discord.gg/46kKJ5VeHt)