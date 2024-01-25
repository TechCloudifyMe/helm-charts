# helm-charts
## install helm
```
curl -fsSL -o get_helm.sh https://raw.githubusercontent.com/helm/helm/main/scripts/get-helm-3
chmod 700 get_helm.sh
export PATH=$PATH:/usr/local/bin
./get_helm.sh
```
## create your 1st chart
```
helm create myapp-chart
```
Do the modifications as per your requirement
## install helm package
```
helm install <release-name> <path/to/your-chart>
ex: helm install myapp myapp-chart
```
## helm command
```
helm list
helm create <chart-name>
helm install myapp myapp-chart
helm upgrade myapp myapp-chart
helm status myapp
helm uninstall myapp
```
## to run same helm chart for multiple application
maintain a seperate values file for each microservice
```
helm install <release-name> <path/to/chart> -f <path/to/values.yaml>
helm install app1 myapp-chart -f /opt/helm-charts/app1/values.yaml
```


## deploy mysql using helm repo

In Helm, a Helm repository (or Helm repo)  serves as a centralized location for storing, sharing, and distributing Helm charts(like docker base image). Helm repositories make it easier to manage and deploy Kubernetes applications
```
helm repo add helm-repo https://charts.bitnami.com/bitnami

```


--links--
https://devopscube.com/create-helm-chart/

**NOTES.txt**: 
The NOTES.txt file in a Helm chart is used to provide post-installation or post-upgrade information and instructions to users. When a Helm chart is installed or upgraded, Helm displays the contents of the NOTES.txt file in the command-line interface to inform users about important details related to the deployment.

**_helper.tpl**: In Helm, the _helpers.tpl file is a convention for creating reusable template functions and definitions that can be shared across multiple templates within the same chart.

ex:
Default Values: You can set default values for variables used throughout your chart. For instance:
```
{{/* _helpers.tpl */}}
{{- define "mychart.labels" -}}
    app: my-app
    release: {{ .Release.Name | quote }}
{{- end }}
```
Now, in other templates, you can include these labels easily:
```
apiVersion: apps/v1
kind: Deployment
metadata:
  name: my-deployment
  labels:
    {{ include "mychart.labels" | nindent 8 }}
```
