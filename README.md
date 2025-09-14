📘 Kubernetes Namespace + Deployment + Service + Endpoints Demo

This guide shows how to deploy an app into a custom namespace, expose it with a Service, check Endpoints, and test using a curl pod.

🚀 1. Create Namespace
kubectl create namespace demo-k8s

📦 2. Deploy Application

Apply the deployment into the namespace:

kubectl apply -f deployment.yml -n demo-k8s

🌐 3. Create Service

Apply the Service definition:

kubectl apply -f services.yml -n demo-k8s


Check the Service:

kubectl get svc nginx-service -n demo-k8s


Check the Endpoints (should list Pod IPs + ports):

kubectl get endpoints nginx-service -n demo-k8s

🔍 4. Run a curl Pod for Testing

Start a temporary curl pod in the same namespace:

kubectl run curl --rm -it --image=curlimages/curl --restart=Never -n demo-k8s -- sh

🌐 5. Test Connectivity (inside the curl pod shell)

Once inside the curl pod, run:

# Replace <endpoint> with either Service name or ClusterIP
curl http://nginx-service:80
OR
# You can also test a specific Pod IP from the Endpoints list
curl http://<endpoint>:80


👉 You should see the Nginx welcome page HTML.

Exit the curl pod:

exit

🧹 6. Cleanup
kubectl delete namespace demo-k8s

✅ What You Learned

How to create and work in a namespace.

How to deploy an app and expose it with a Service.

How to verify Endpoints that map to Pod IPs.

How to test connectivity using a temporary curl pod.