1. Verify that the Kiali service has healthy endpoints:
`kubectl get endpoints kiali -n istio-system`
This will show whether Kiali has any healthy backend pods that are ready to receive traffic.
If there are no endpoints or the wrong endpoints are listed, the service won't be able to route traffic to Kiali.

2. check the Kiali pod logs to identify issues:
`kubectl logs -l app=kiali -n istio-system`

3. Check the istio gateway logs
`kubectl get pods -l istio=pilot -n istio-system`

4. Test kiali availbity withing the clsuer
`kubectl run test-pod --rm -it --image=busybox --restart=Never -- wget -qO- http://kiali.istio-system.svc.cluster.local:20001/kiali`


if you get html connect it means kiali is u and runningan acesible withinht elcster



chekc connetiny from istion gateway pod
kubectl exec -it <ingressgateway-pod-name> -n istio-system -- curl kiali.istio-system.svc.cluster.local:20001



`apply nodeport.yaml`


install poemteu-kube oeprator 

Add the Prometheus community Helm repository
helm repo add prometheus-community https://prometheus-community.github.io/helm-charts

Install Prometheus Operator using Helm
helm install prometheus prometheus-community/kube-prometheus-stack -n monitoring



and update kiali config map
`kubectl edit configmap kiali -n istio-system`


and add
```
external_services:
  prometheus:
    url: "http://prometheus-kube-prometheus-prometheus.monitoring.svc.cluster.local:9090"
```


restart kiali
kubectl rollout restart deployment kiali -n istio-system




or use this

https://istio.io/latest/docs/ops/integrations/prometheus/#option-1-quick-start