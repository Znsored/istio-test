apiVersion: networking.istio.io/v1alpha3
kind: VirtualService
metadata:
  name: my-application
spec:
  hosts:
  - "*"
  gateways:
  - k8s-ingress-gateway
  http:
  - match:
    - uri:
        prefix: /kiali
    route:
    - destination:
        host: my-application-svc
        port:
          name: http


apiVersion: networking.istio.io/v1alpha3
kind: Gateway
metadata:
  name: istio-system-ingress-gateway
  namespace: istio-system
spec:
  selector:
    istio: pilot
  servers:
  - port:
      name: http
      number: 80
      protocol: HTTP
    hosts:
    - "*"