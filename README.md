# odoo:8.0-debain 10
Custom Odoo 8.0 installation with debain 10 and docker. 
Before installing odoo there are two python packages which does not install in debain 10. we need to make dummy package for them. 
- python-pypdf
- python-imaging_1.13
#### Steps of creating fake package
```bash
apt-get install equivs  
run equivs-control python-pypdf # will create and populate the file python-pypdf in current directory
```

* Edit python-pypdf file
**Note:** dot and space under "Description" are mandatory 
```
Section: python
Package: python-pypdf
Version: 1.13
Description: fake package to provide python-pypdf
Description: fake package to provide python-pypdf
 python-pypdf will need to be installed with pip
 .
 python-pypdf2  does not provide python-pypdf
 ```
* Run following bash command
```bash
run equivs-build python-pypdf # will create the fake package python-pypdf_1.13_all.deb
dpkg -i python-pypdf_1.13_all.deb # install the package 
pip install pyPdf 
```

- Above step will helps you to create fake package for python-pypdf. Please use same step for python-imaging_1.13 also.
- now install odoo in debain buster

# Steps using docker
* Clone [odoo-8.0](https://github.com/gmanandhar/odoo-8.0.git)
* Install Docker in your host
* Run below commands
```bash
docker --version #Check docker verison and verify correctly installed
docker run -d -e POSTGRES_USER=odoo -e POSTGRES_PASSWORD=odoo -e POSTGRES_DB=postgres --name db postgres:10 # Install postgres database in another container
docker build -t <image-name> . #Before using this command working directory should have Dockerfile
docker images #Check image is installed or not
docker run -p 8069:8069 --name <container-name> --link db:db -t <container-name>
```
**Note:** I am using external database and skipping fake package installation. You can directly copy the packages and run from dpkg

