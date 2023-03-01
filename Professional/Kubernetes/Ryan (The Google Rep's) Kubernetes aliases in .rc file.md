```
k=kubectl
kcur='kubectl config current-context && kubectl config view --minify | grep namespace:|tr -d " "'
kdp='k describe pod'
kexec='kubectl exec -ti   -- /bin/bash'
kgc='kubectl get pods -o jsonpath={.items[*].spec.containers[*].name}'
kge='kubectl get events --sort-by='\''.lastTimestamp'\'
kgi='kubectl get pods -o jsonpath="{..image}"| tr " " "\n"|sort -u '
kgp='kubectl get pod'
khpa='kubectl get hpa'
kn=kubens
krestart='kubectl rollout restart deployment'
kx=kubectx
```
