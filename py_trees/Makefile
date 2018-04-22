#############################################################################################
# Build Documentation
#############################################################################################

NAME=`./setup.py --name`
VERSION=`./setup.py --version`
# LOCAL_DIR = $(shell pwd)/doc/html/
# REMOTE_DIR:=files@files.yujin.com:shared/documentation/${NAME}/${VERSION}
# REMOTE_SSH:=files@files.yujin.com
#docs:
#	rosdoc_lite .
#
#details:
#	@echo ${VERSION}
#	@echo ${NAME}
#
#upload:
#	ssh ${REMOTE_SSH} 'mkdir -p shared/documentation/${NAME}/${VERSION}; rm -f shared/documentation/${NAME}/latest; ln -sf ${VERSION} shared/documentation/${NAME}/latest'
#	rsync --delete --recursive --links --verbose ${LOCAL_DIR} ${REMOTE_DIR}


help:
	@echo "Local Build"
	@echo "  deps      : install various build dependencies"
	@echo "  build     : build the python package"
	@echo "  tests     : run all of the nosetests"
	@echo "  clean     : clean build/dist directories"
	@echo "Packages"
	@echo "  pypi      : upload the package to PyPI"
	@echo "  source_deb: source packaging (for ppas)"
	@echo "  deb       : build the deb"
	@echo "Documentation"
	@echo "  docs      : buidl sphinx documentation"

docs:
	PY_TREES_DISABLE_COLORS=1 sphinx-build -b html doc doc/html

build:
	python setup.py build

deps:
	echo "Downloading dependencies"
	sudo apt-get install python-stdeb virtualenvwrapper

clean:
	-rm -f MANIFEST
	-rm -rf build dist
	-rm -rf deb_dist
	-rm -rf debian
	-rm -rf ../*.build
	-rm -rf *.tar.gz
	-rm -rf *.egg-info

source_package:
	python setup.py sdist

source_deb:
	rm -rf dist deb_dist
	python setup.py --command-packages=stdeb.command sdist_dsc

deb:
	rm -rf dist deb_dist
	python setup.py --command-packages=stdeb.command bdist_deb

pypi: 
	python setup.py sdist upload

tests:
	python setup.py test

.PHONY: tests clean
