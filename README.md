# HelloWorld
net3.x HelloWorld app, version BL/Inspections currently using

### source
found an old helloworld app based on netcore 3.x framework. https://github.com/cloudfoundry-samples/dotnet-core-hello-world

## Image build and run

### login to github packages

Create a github personal access token w/ read privileges to github packages. Instructions: https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/creating-a-personal-access-token


### build and run the image
These assume you are running on M1 chip (amd64), if you are not then remove the following from the build and run commands
`--platform=linux/amd64`

#### netcore 3.1
```
export GITHUB_TOKEN=<your github token>
$ cat $GITHUB_TOKEN | docker login ghcr.io -u <your github username> --password-stdin
$ docker build -t helloworld-netcore-3 --build-arg GITHUB_TOKEN=$GITHUB_TOKEN --platform=linux/amd64 -f deployment/Dockerfile .
$ docker run -it -p 8080:5000 --platform=linux/amd64 helloworld-netcore-3:latest
Hosting environment: Production
Content root path: /helloworld
Now listening on: http://localhost:5000
```

#### netcore 6.0 
```
export GITHUB_TOKEN=<your github token>
$ cat $GITHUB_TOKEN | docker login ghcr.io -u <your github username> --password-stdin
$ docker build -t helloworld-netcore-6 --build-arg GITHUB_TOKEN=$GITHUB_TOKEN --platform=linux/amd64 -f deployment/Dockerfile-6.0 .
$ docker run -it -p 8080:5000 --platform=linux/amd64 helloworld-netcore-6:latest
Hosting environment: Production
Content root path: /helloworld
Now listening on: http://localhost:5000
```

Browse to http://localhost:8080

## For later
deployment manifest [example](https://github.com/BuildingLink/Amenities/blob/master/deployment/fleet/dev/deployment-api.yaml)