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


### build the image
```
export GITHUB_TOKEN=<your github token>
$ cat $GITHUB_TOKEN | docker login ghcr.io -u <your github username> --password-stdin
$ docker build -t helloworld-net-6 --build-arg GITHUB_TOKEN=$GITHUB_TOKEN -f deployment/Dockerfile .
```

This results in the following build error
```
 > [build 7/7] RUN dotnet build HelloWorld/HelloWorld.csproj -c Release:
#13 1.350 MSBuild version 17.3.2+561848881 for .NET
#13 7.315   Determining projects to restore...
#13 9.382   All projects are up-to-date for restore.
#13 22.44 CSC : error CS5001: Program does not contain a static 'Main' method suitable for an entry point [/src/HelloWorld/HelloWorld.csproj]
#13 22.53
#13 22.53 Build FAILED.
#13 22.53
#13 22.53 CSC : error CS5001: Program does not contain a static 'Main' method suitable for an entry point [/src/HelloWorld/HelloWorld.csproj]
#13 22.53     0 Warning(s)
#13 22.53     1 Error(s)
#13 22.53
#13 22.53 Time Elapsed 00:00:20.44
```

## For later
deployment manifest [example](https://github.com/BuildingLink/Amenities/blob/master/deployment/fleet/dev/deployment-api.yaml)