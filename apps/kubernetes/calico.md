# Calico kubernetes network provider

## Running `calicoctl` as pod

```
kubectl apply -f -<<EOF
apiVersion: v1
kind: Pod
metadata:
  name: calicoctl 
  namespace: kube-system
spec:
  hostNetwork: true
  containers:
  - name: calicoctl
    image: calico/ctl:v1.0.1
    command: ["/bin/sh", "-c", "while true; do sleep 3600; done"]
    env:
    - name: ETCD_ENDPOINTS
      valueFrom:
        configMapKeyRef:
          name: calico-config
          key: etcd_endpoints
EOF

$ kubectl exec -ti -n kube-system calicoctl -- /calicoctl get profiles -o wide
```

## Prevent egress traffic for namespace

Sometimes you want to block internet access for container. You can do that with
calico policy.

```
calicoctl apply -f - <<EOF
apiVersion: v1
kind: policy
metadata:
  name: advanced-policy-demo.deny-egress
spec:
  selector: calico/k8s_ns == 'advanced-policy-demo'
  order: 500
  egress:
  - action: deny
    destination:
      notSelector: calico/k8s_ns == 'advanced-policy-demo'
EOF
```

This will block all pods in namespace `advanced-policy-demo`.

If you want to whitelist some traffic, do following:

```
calicoctl apply -f - <<EOF
apiVersion: v1
kind: policy
metadata:
  name: advanced-policy-demo.allow-dns
spec:
  selector: has(calico/k8s_ns)
  order: 400
  egress:
  - action: allow
    protocol: udp
    destination:
      selector: calico/k8s_ns == 'kube-system' && k8s-app == 'kube-dns'
      ports: [53]
EOF
```

This whitelists DNS traffic for kube-dns.
