# How to store a Docker image in my Google Cloud Artifact Registry repo

## 1. Create a Google Cloud Artifact Registry repo


## 2. Create a .NET8 WebAPI and create the Dockerfile




This is the Dockerfile source code:

```
#See https://aka.ms/customizecontainer to learn how to customize your debug container and how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:8.0 AS base
USER app
WORKDIR /app
EXPOSE 8080
EXPOSE 8081

FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
ARG BUILD_CONFIGURATION=Release
WORKDIR /src
COPY ["GoogleCloudWebAPI.csproj", "."]
RUN dotnet restore "./././GoogleCloudWebAPI.csproj"
COPY . .
WORKDIR "/src/."
RUN dotnet build "./GoogleCloudWebAPI.csproj" -c $BUILD_CONFIGURATION -o /app/build

FROM build AS publish
ARG BUILD_CONFIGURATION=Release
RUN dotnet publish "./GoogleCloudWebAPI.csproj" -c $BUILD_CONFIGURATION -o /app/publish /p:UseAppHost=false

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "GoogleCloudWebAPI.dll"]
```

## 2. Create the Docker image



```
docker build -t your-webapi-image-name .
```

## 3. Tag the Docker imge

my-location: europe-southwest1

my-gcloud-project: extreme-axon-381209

my-repo: myfirstrepo

my-imagename: your-webapi-image-name:v1.0

```
docker tag your-webapi-image-name:latest europe-southwest1-docker.pkg.dev/extreme-axon-381209/myfirstrepo/your-webapi-image-name:v1.0
```

## 4. Push the Docker image to Google Cloud Artifact Registry repo

### 4.1. Authenticate gcloud:

Make sure you're authenticated with the Google Cloud SDK and that you're using the correct project. Run:

```
gcloud auth login
```

```
gcloud config set project extreme-axon-381209
```

### 4.2. Configure Docker to Use gcloud as a Credential Helper:

Run the following command to configure Docker to use gcloud as the credential helper:

```
gcloud auth configure-docker europe-southwest1-docker.pkg.dev
```

This command updates your Docker configuration to use gcloud as the credential helper for repositories in europe-southwest1-docker.pkg.dev

### 4.3. Push Docker image to Google Cloud Artifact Registry repo

```
docker push europe-southwest1-docker.pkg.dev/extreme-axon-381209/myfirstrepo/your-webapi-image-name:v1.0
```

## 4.4. Veryfy the Google Cloud Docker image in Docker Desktop

We pull the Docker image from Google Cloud Artifact Registry repo

```
docker pull europe-southwest1-docker.pkg.dev/extreme-axon-381209/myfirstrepo/your-webapi-image-name:v1.0
```

We run the Docker image in Docker Destop

```
docker run -p 8080:8080 -p 8081:8081 europe-southwest1-docker.pkg.dev/extreme-axon-381209/myfirstrepo/your-webapi-image-name:v1.0
```

http://localhost:8080/weatherforecast

![image](https://github.com/luiscoco/GoogleCloud_Sample10-Artifact-Registry/assets/32194879/57553f3b-04b2-4baf-8603-1747b07ad527)

## 5. Deploying the Docker image

```
gcloud run deploy --image gcr.io/your-project-id/your-image-name
```

