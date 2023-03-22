 More information about 
 [Container Registry documentation ](https://cloud.google.com/container-registry/docs/pushing-and-pulling) 

Google Container Registry (GCR) is a managed Docker registry provided by Google Cloud Platform that makes it easy to store and manage Docker images for Kubernetes deployments. GCR is fully integrated with Kubernetes, which makes it a popular choice for storing and deploying Docker images on Kubernetes.

Here are the steps to use GCR in Kubernetes:

1. First, you need to create a Docker image of your application. You can use Dockerfile to create a Docker image or use a pre-built image from Docker Hub.

2. Once you have the Docker image, you need to tag it with the GCR registry name. The registry name is in the format gcr.io/[PROJECT-ID]/[IMAGE]:[TAG]. The [PROJECT-ID] is the ID of the Google Cloud Platform project, and the [IMAGE] is the name of the Docker image you want to push to the registry. The [TAG] is the version number of the Docker image.

3. Authenticate to GCR using the Docker command line tool. Run the following command to authenticate:

- `gcloud auth login`
- `gcloud auth configure-docker`

4. Push the Docker image to GCR using the Docker command line tool. Run the following command to push the image to GCR:

- `docker push gcr.io/[PROJECT-ID]/[IMAGE]:[TAG]`

5. Once the Docker image is pushed to GCR, you can use it in your Kubernetes deployment. In the Kubernetes deployment YAML file, specify the image name as the GCR registry name. Here's an example YAML file:

``` yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: my-app
spec:
  replicas: 1
  selector:
    matchLabels:
      app: my-app
  template:
    metadata:
      labels:
        app: my-app
    spec:
      containers:
      - name: my-app
        image: gcr.io/[PROJECT-ID]/[IMAGE]:[TAG]
        ports:
        - containerPort: 8080
```

6. Apply the deployment YAML file using the Kubernetes command line tool. Run the following command to apply the YAML file:

- `kubectl apply -f deployment.yaml`

That's it! Your Kubernetes deployment should now use the Docker image stored in GCR.