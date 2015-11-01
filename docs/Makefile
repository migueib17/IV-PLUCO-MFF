#Makefile autor: Miguel Fdez Fdez
all: test doc run
clean:
	rm -rf *~* && find . -name '*.pyc' -exec rm {} \;
	rm -rf docs/*

test:
	nosetests
doc:
	pyccoon
run:
	python _index_.py runserver 0.0.0.0:1111
