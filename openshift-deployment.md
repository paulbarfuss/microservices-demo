# Create a microservices-demo namespaces

```bash
oc new-project microservices-demo-mesh
oc new-project microservices-demo
```

# Install ArgoCD operator

From the OpenShift OperatorHub, install the following:

- Red Hat OpenShift GitOps

```bash
oc apply -k https://github.com/redhat-cop/gitops-catalog/openshift-gitops-operator/overlays/stable
```

There will be a default ArgoCD instance in the openshift-gitops namespace. Check the instance and its route to get to the ArgoCD console:

```bash
oc get argocd -n openshift-gitops
oc get route -n openshift-gitops-server -n openshift-gitops
```

# Install Service Mesh Operators

Install Red Hat OpenShift Service Mesh and a default instance in the istio-system namespace:

```bash
oc apply -k https://github.com/redhat-cop/gitops-catalog/openshift-servicemesh/operator/overlays/stable
```

Ensure the ServiceMeshControlPlane CRD exists before installing an instance:

```bash
oc get crd servicemeshcontrolplanes.maistra.io
oc apply -k https://github.com/redhat-cop/gitops-catalog/openshift-servicemesh/instance/overlays/default
oc get servicemeshcontrolplane istio-system -n istio-system
```

# Install Tekton

Install Red Hat OpenShift Pipelines operator

```bash
oc apply -k https://github.com/redhat-cop/gitops-catalog/openshift-pipelines-operator/overlays/stable
```
