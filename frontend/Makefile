.PHONY: clean build run

run: build
	docker run --rm -it -p 80:80 realengine/designer:build

build:
	docker build -t realengine/designer:build real-designer

clean:
	docker rmi realengine/designer:build | true

shell:
	docker run --rm -it realengine/designer:build bash
