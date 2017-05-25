# LABOPS

automating server deploy for beeva labs experiments

## why?

our experiments should be _easily_ repeatable by anyone interested

documentation is well and good, but code is better

## how?

instead of a README with instructions to manually install and configure the needed software, we can use 'devops' technologies to describe the environment used for the experiment in a repeatable and testable way

## technologies

* VM/instance creation: [packer](https://packer.io)
* VM/instance provisioning:
  * [ansible](https://ansible.com)
  * [fabric](https://fabfile.org) (not integrated with packer, so it must be a manual step)
  * shell script
  * ...
* multi-instance deployments:
  * [terraform](https://terraform.io)
* software installation
  * [docker](https://docker.com)
  * ...

these are just recommendations! if you feel more confortable using Makefile, or a go program, or cmake + salt + FORTRAN ... please do! but a README with manual steps should be our last resort.
