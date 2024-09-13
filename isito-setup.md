install helm from the link "https://helm.sh/docs/intro/install/"


From Apt (Debian/Ubuntu)

```bash
curl https://baltocdn.com/helm/signing.asc | gpg --dearmor | sudo tee /usr/share/keyrings/helm.gpg > /dev/null
sudo apt-get install apt-transport-https --yes
echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/helm.gpg] https://baltocdn.com/helm/stable/debian/ all main" | sudo tee /etc/apt/sources.list.d/helm-stable-debian.list
sudo apt-get update
sudo apt-get install helm
```


Install Isito from "https://istio.io/latest/docs/setup/install/helm/"

Configure the Helm repository:

```bash
helm repo add istio https://istio-release.storage.googleapis.com/charts
helm repo update
```

1. Create the namespace, istio-system, for the Istio components:
```kubectl create namespace istio-system```

2. Install the Istio base chart which contains cluster-wide Custom Resource Definitions (CRDs) which must be installed prior to the deployment of the Istio control plane
```helm install istio-base istio/base -n istio-system --set defaultRevision=default```

3. Validate the CRD installation with the helm ls command:
```helm ls -n istio-system```

4. Install the Istio discovery chart which deploys the istiod service:
```helm install istiod istio/istiod -n istio-system --wait```

5. Verify the Istio discovery chart installation:
```helm ls -n istio-system```

6. Check istiod service is successfully installed and its pods are running:
```kubectl get deployments -n istio-system --output wide```



install kiali
```kubectl apply -f https://raw.githubusercontent.com/istio/istio/release-1.23/samples/addons/kiali.yaml```

