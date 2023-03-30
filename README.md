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

#### BL netcore 3.1
```
export GITHUB_TOKEN=<your github token>
$ echo $GITHUB_TOKEN | docker login ghcr.io -u <your github username> --password-stdin
$ docker build -t helloworld-netcore-3 --build-arg GITHUB_TOKEN=$GITHUB_TOKEN --platform=linux/amd64 -f deployment/Dockerfile-3.1 .
$ docker run -it -p 8080:80 -e ASPNETCORE_URLS=http://+:80 --platform=linux/amd64 helloworld-netcore-3:latest
Hosting environment: Production
Content root path: /helloworld
Now listening on: http://localhost:5000
```

#### BL netcore 6.0 
```
export GITHUB_TOKEN=<your github token>
$ echo $GITHUB_TOKEN | docker login ghcr.io -u <your github username> --password-stdin
$ docker build -t helloworld-netcore-6 --build-arg GITHUB_TOKEN=$GITHUB_TOKEN --platform=linux/amd64 -f deployment/Dockerfile-6.0 .
$ docker run -it -p 8080:80 -e ASPNETCORE_URLS=http://+:80 --platform=linux/amd64 helloworld-netcore-6:latest
warn: Microsoft.AspNetCore.DataProtection.KeyManagement.XmlKeyManager[35]
      No XML encryptor configured. Key {2a78d845-7727-48c3-862c-53360a1a18b6} may be persisted to storage in unencrypted form.
info: Microsoft.Hosting.Lifetime[14]
      Now listening on: http://[::]:80
info: Microsoft.Hosting.Lifetime[0]
      Application started. Press Ctrl+C to shut down.
info: Microsoft.Hosting.Lifetime[0]
      Hosting environment: Production
info: Microsoft.Hosting.Lifetime[0]
      Content root path: /helloworld/
```

#### BL ms netcore images
```
export GITHUB_TOKEN=<your github token>
$ docker build -t helloworld-ms-netcore-6 --build-arg GITHUB_TOKEN=$GITHUB_TOKEN -f deployment/Dockerfile-ms-6.0 .
$ docker run -it -p 8080:80 -e ASPNETCORE_hostBuilder__reloadConfigOnChange=false helloworld-ms-netcore-6:latest
warn: Microsoft.AspNetCore.DataProtection.Repositories.FileSystemXmlRepository[60]
      Storing keys in a directory '/root/.aspnet/DataProtection-Keys' that may not be persisted outside of the container. Protected data will be unavailable when container is destroyed.
warn: Microsoft.AspNetCore.DataProtection.KeyManagement.XmlKeyManager[35]
      No XML encryptor configured. Key {9e86edba-9069-42e0-a289-cb2449dece9f} may be persisted to storage in unencrypted form.
info: Microsoft.Hosting.Lifetime[14]
      Now listening on: http://[::]:80
info: Microsoft.Hosting.Lifetime[0]
      Application started. Press Ctrl+C to shut down.
info: Microsoft.Hosting.Lifetime[0]
      Hosting environment: Production
info: Microsoft.Hosting.Lifetime[0]
      Content root path: /helloworld/
```

Browse to http://localhost:8080

## For later
deployment manifest [example](https://github.com/BuildingLink/Amenities/blob/master/deployment/fleet/dev/deployment-api.yaml)