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

```
docker push gcr.io/your-project-id/your-image-name
```


## 5. Deploying the Docker image

```
gcloud run deploy --image gcr.io/your-project-id/your-image-name
```

