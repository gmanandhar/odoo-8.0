# odoo:8.0-debain 10
Custom Odoo 8.0 with debain 10 using docker
Before installing odoo there are two python packages which does not install in debain 10. we need to make dummy package for them. 
 python-pypdf
 python-imaging_1.13
# Steps of creating fake package
> apt-get install equivs  
> run equivs-control python-pypdf # will create and populate the file python-pypdf in current directory

# Edit python-pypdf file (dot and space under "Description" are mandatory) 
>Section: python
>Package: python-pypdf
>Version: 1.13
>Description: fake package to provide python-pypdf
>Description: fake package to provide python-pypdf
> python-pypdf will need to be installed with pip
> .
> python-pypdf2  does not provide python-pypdf

> run equivs-build python-pypdf #will create the fake package python-pypdf_1.13_all.deb
> dpkg -i python-pypdf_1.13_all.deb #install the package 
> pip install pyPdf 

# Above step will helps you to create fake package for python-pypdf. Please use same step for python-imaging_1.13 also.
# now install odoo in debain buster

