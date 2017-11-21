.PHONY: clean build run

build:
	docker build -t realengine/frontend:build .

clean:
	docker rmi realengine/frontend:build | true

run:

shell:
	docker run --rm -it realengine/frontend:build bash
