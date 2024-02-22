# k8s-jenkins-quickstart
Install Prometheus Operator CRD first:
```bash
curl -sL https://github.com/prometheus-operator/prometheus-operator/releases/download/v0.71.2/bundle.yaml | kubectl -n default create -f -
```
Deploy Jenkins:
```bash
helm repo add jenkins https://charts.jenkins.io
helm install --version 5.0.15 -n default -f values.yaml jenkins jenkins/jenkins
```

Get admin password:
```bash
kubectl exec --namespace default -it svc/jenkins -c jenkins -- /bin/cat /run/secrets/additional/chart-admin-password && echo
```

Visit web UI:
```
kubectl --namespace default port-forward svc/jenkins 8080:8080
```
Login with the username `admin` and the password you have obtained.

The chart only deploys a ServiceMonitor, a CRD managed by the Prometheus Operator. This ServiceMonitor expects metrics from the `/prometheus` endpoint of the Jenkins controller. However, you need to manually add the Prometheus plugin to your Jenkins instance and restart it for proper integration. You can find the Prometheus plugin here: https://plugins.jenkins.io/prometheus
