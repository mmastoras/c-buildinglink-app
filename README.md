# HelloWorld
net3.x HelloWorld app, version BL/Inspections currently using

### source
found an old helloworld app based on netcore 3.x framework. https://github.com/cloudfoundry-samples/dotnet-core-hello-world

## Image build and run

### login to github packages

Create a github personal access token w/ read privileges to github packages. Instructions: https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/creating-a-personal-access-token


### build and run the image
```
export GITHUB_TOKEN=<your github token>
$ cat $GITHUB_TOKEN | docker login ghcr.io -u <your github username> --password-stdin
$ docker build -t helloworld-aspnet-3 --build-arg GITHUB_TOKEN=$GITHUB_TOKEN -f deployment/Dockerfile .
$ docker run -it -p 8080:5000 helloworld-aspnet-3:latest
Hosting environment: Production
Content root path: /helloworld
Now listening on: http://localhost:5000
```

Browse to http://localhost:8080

## For later
deployment manifest [example](https://github.com/BuildingLink/Amenities/blob/master/deployment/fleet/dev/deployment-api.yaml)