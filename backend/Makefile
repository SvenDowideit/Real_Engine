.PHONY: clean build run exec

build:
	docker build -t realengine/backend:build .

clean:
	docker rmi realengine/backend:build | true

run:
	docker run --name re-backend -p 8080:8080 --rm realengine/backend:build

exec:
	docker exec -it re-backend bash


