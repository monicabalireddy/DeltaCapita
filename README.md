# CI/CD Pipeline
The ci-cd.yml wokrlfow triggers on push and Pr to main. It runs npm install and npm test. Deploys to kubernetes using AWS EKS and kubectl. 
# Kubernetes Manifests
clients-api.yml: 
    Deployment for the Clients API (using a public image).
    Service (ClusterIP) for the API
cert-manager.yml:
    ClusterIssuer for Let’s Encrypt.
    Certificate for clients.api.deltacapita.com
ingress.yml:
    Ingress resource for routing and TLS.
    References the certificate and uses the NGINX ingress class.
mongodb.yml:
    This sets up a MongoDB Deployment and exposes it via a Service in the clients-api namespace.

# Note
This pipeline is a basic version that has been deployed on a EKS cluster that has been set up on a personal AWS account. The failures encountered in the last runs have been addressed locally through kubectl troubleshooting. With proper resources a much better pipleine cab be created where the secrets will be managed on Vault, the images will be platform images built through Docker according to enterprise standards. For efficient CI the Docker image can be built and pushed to Artifactory, and fetched from there through image pull for deployment. A custom values.yml file can be designed for dedicated set of helm charts for all the k8s services and the values can be overwritten using the values the user wants. This pipeline isn't a much sophesticated version due to limited access to tools. 