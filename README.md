# HelloWorld
net6.0 HelloWorld app.

### source
this created a web app that failed to build in the way BL is building in their docker images so....

ran the following to create the C# code for a simply web app, assumes you have net6.0 installed locally
```
$ dotnet new webapp -o HelloWorld --no-https -f net6.0
```

### next attempt
this also doesn't create anything looking like the BL source, particular they are missing the main() which is what the build error 

```
$ dotnet new console -o HelloWorld -f net6.0
```

## Image 

### login to github packages

Create a github personal access token w/ read privileges to github packages. Instructions: https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/creating-a-personal-access-token


### build and run the image
```
export GITHUB_TOKEN=<your github token>
$ cat $GITHUB_TOKEN | docker login ghcr.io -u <your github username> --password-stdin
$ docker build -t helloworld-aspnet-3 --build-arg GITHUB_TOKEN=$GITHUB_TOKEN -f deployment/Dockerfile .
$ docker run -it -p 8080:5000 helloworld-aspnet-3:latest
```


## For later
deployment manifest [example](https://github.com/BuildingLink/Amenities/blob/master/deployment/fleet/dev/deployment-api.yaml)