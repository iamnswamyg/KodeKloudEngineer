The Nautilus DevOps team is working on to setup some pre-requisites for an application that will send the greetings to different users. There is a sample deployment, that needs to be tested. Below is a scenario which needs to be configured on Kubernetes cluster. Please find below more details about it.
1.Create a pod named print-envars-greeting.
2.Configure spec as, the container name should be print-env-container and use bash image.
3.Create three environment variables:
a. GREETING and its value should be Welcome to
b. COMPANY and its value should be Stratos
c. GROUP and its value should be Datacenter
Use command to echo ["$(GREETING) $(COMPANY) $(GROUP)"] message.
You can check the output using <kubctl logs -f [ pod-name ]> command.
Note: The kubectl utility on jump_host has been configured to work with the kubernetes cluster.

```
kubectl get pods
vi /tmp/env.yml
[
apiVersion: v1
kind: Pod
metadata:
  name: print-envars-greeting
  labels:
    name: print-envars-greeting
spec:
  containers:
    - name: print-env-container
      image: bash
      env:
        - name: GREETING
          value: "Welcome to"
        - name: COMPANY
          value: "Stratos"
        - name: GROUP
          value: "Datacenter"
      command: ["echo"]
      args: ["$(GREETING) $(COMPANY) $(GROUP)"]
      
      
]
cat /tmp/env.yml
kubectl create -f /tmp/env.yml
kubectl get pods
kubectl logs print-envars-greeting
```