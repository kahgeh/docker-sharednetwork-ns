# Build
cd serviceA
docker build . -t=servicea

cd ../serviceB
docker build . -t=serviceb

# Run 
## start servicea normally
docker run -d --rm --name=servicea -e CONTAINER_NAME=servicea servicea

## specify --network=container:servicea when starting serviceb
docker run -d --rm --network=container:servicea -e CONTAINER_NAME=serviceb --name=serviceb serviceb

# Test effect of sharing same network namespace 

Connect to servicea container : `docker exec -it servicea sh`

Observe how it's possible to use localhost to connect serviceb's app
```
/app # curl localhost:8080
{ "hello from": "servicea" }
/app # curl localhost:8081
{ "hello from": "serviceb" }
```