# Istio requires more resources to run; Minikube starts with 1 cluster by default, we would need much more than that.

minikube start --cpus 6 --memory 8192

# Add istioctl bin to Path, istioctl is accessible

# Install istio inside minikube cluster

# Get Namespace
kubectl get ns

# Get Pods 
kubectl get pod


#Output 

-----------------------------------------------------------------------------
(base) SVN-19-409-mohamedfazaary:istio mohamedfazaary$ istioctl install
Detected that your cluster does not support third party JWT authentication. Falling back to less secure first party JWT. See https://istio.io/v1.10/docs/ops/best-practices/security/#configure-third-party-service-account-tokens for details.
! values.global.jwtPolicy is deprecated; use Values.global.jwtPolicy=third-party-jwt. See http://istio.io/latest/docs/ops/best-practices/security/#configure-third-party-service-account-tokens for more information instead
This will install the Istio 1.10.0  profile with ["Istio core" "Istiod" "Ingress gateways"] components into the cluster. Proceed? (y/N) yes
✔ Istio core installed                                                                                         
- Processing resources for Istiod. Waiting for Deployment/istio-system/istiod                                  
✔ Istiod installed                                                                                             
- Processing resources for Ingress gateways. Waiting for Deployment/istio-system/istio-ingressgateway          
✔ Ingress gateways installed                                                                                   
✔ Installation complete  
-----------------------------------------------------------------------------


# Validate NS creation as well as Pod that is created within the NS specified.

kubectl get ns
(Pods)
kubectl get pod -n istio-system



# Demo - GCP Project  
https://github.com/GoogleCloudPlatform/microservices-demo


Locate & Apply the Manifest K8s manifest (8mins to come up)

kubectl apply -f kubernetes-manifests.yaml [ DONT DO IT IF YOUR CLUSTER IS SLOW ]

# Configure ISTIO to insert Sidecars into the Pod


# Label your Namespaces - This is critical for Istio to work

```
kubectl get ns default --show-labels
```

kubectl label namespace default k:v
```
kubectl label namespace default istio-injection=enabled
```

ONCE LABEL IS ADDED, Run the following

```
kubectl apply -f kubernetes-manifests.yaml
```

kubectl apply -f istio-1.10.0/samples/addons/

Apply the integrations such as Grafana, Prometheus etc.

---
kubectl get pods -n istio-system
---

To access pods, we need services.
Check that,
---
kubectl get svc -n istio-system
---


Port forwarding on Kiali

```
kubectl port-forward svc/kiali -n istio-system 20001
```

# Note on the labels 
app: =-> When deploying Microservices in ISTIO, we need the app label for data visualisation to work.


