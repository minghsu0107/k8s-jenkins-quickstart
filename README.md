# k8s-jenkins-quickstart
Deploy Jenkins:
```bash
helm repo add jenkins https://charts.jenkins.io
helm install jenkins jenkins/jenkins --version 4.1.13 -f values.yaml -n default
```

Get admin password:
```bash
kubectl exec --namespace default -it svc/jenkins -c jenkins -- /bin/cat /run/secrets/additional/chart-admin-password && echo
```

Visit web UI:
```
kubectl --namespace default port-forward svc/jenkins 8080:8080
```
Finally, login with the username `admin` and the password you have obtained.