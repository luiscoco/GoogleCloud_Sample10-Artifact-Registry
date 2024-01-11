# How to store a Docker image in my Google Cloud Artifact Registry repo

## 1. Create a Google Cloud Artifact Registry repo



## 2. Create the Docker image


## 3. Tag the Docker imge

my-location:

my-gcloud-project:

my-repo: 

```
docker tag myapp us-central1-docker.pkg.dev/my-gcloud-project/my-repo/myapp:v1.0
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

```

## 5. Deploying the Docker image

```
gcloud run deploy --image gcr.io/your-project-id/your-image-name
```

