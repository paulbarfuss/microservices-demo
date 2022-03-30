# Install Online Boutique in Openshift

## Install Operators

### Install ArgoCD Operator

Install Red Hat OpenShift GitOps operator

```bash
oc apply -k https://github.com/redhat-cop/gitops-catalog/openshift-gitops-operator/overlays/stable
```

There will be a default ArgoCD instance in the openshift-gitops namespace. Check the instance and its route to get to the ArgoCD console:

```bash
oc get argocd -n openshift-gitops
oc get route -n openshift-gitops-server -n openshift-gitops
```

### Install Service Mesh Operators

Install Red Hat OpenShift Service Mesh and a default istio-system namespace

```bash
oc apply -k https://github.com/redhat-cop/gitops-catalog/openshift-servicemesh/operator/overlays/stable
```

Install Elasticsearch Operator

```bash
oc apply -k https://github.com/redhat-cop/gitops-catalog/elasticsearch-operator/overlays/stable
```

Install Kiali and Jaeger Operators


```bash
oc apply -k https://github.com/redhat-cop/gitops-catalog/kiali-operator/overlays/stable
oc apply -k https://github.com/redhat-cop/gitops-catalog/jaeger-operator/overlays/stable

```


Ensure the ServiceMeshControlPlane CRD exists before installing an instance of Service Mesh

```bash
oc get crds servicemeshcontrolplanes.maistra.io
oc apply -k https://github.com/redhat-cop/gitops-catalog/openshift-servicemesh/instance/overlays/default
oc get servicemeshcontrolplane istio-system -n istio-system
```

### Install Tekton

**TODO: Add build and deploy steps as Tekton Pipelines**

Install Red Hat OpenShift Pipelines operator

```bash
oc apply -k https://github.com/redhat-cop/gitops-catalog/openshift-pipelines-operator/overlays/stable
```

## Deploy ArgoCD App of Apps

```bash
oc create -f app-of-apps.yaml
```

### Visit the Online Boutique Shop

Run the following command to get the Openshift Route for the new Istio Ingress Gateway

```bash
oc -n istio-system get route istio-ingressgateway -o jsonpath='{.spec.host}'
```
