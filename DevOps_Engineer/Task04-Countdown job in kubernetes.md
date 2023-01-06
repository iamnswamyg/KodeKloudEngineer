The Nautilus DevOps team is working on to create few jobs in Kubernetes cluster. They might come up with some real scripts/commands to use, but for now they are preparing the templates and testing the jobs with dummy commands. Please create a job template as per details given below:
Create a job countdown-datacenter.
The spec template should be named as countdown-datacenter (under metadata), and the container should be named as container-countdown-datacenter
Use image ubuntu with latest tag only and remember to mention tag i.e ubuntu:latest, and restart policy should be Never.
Use command for i in ten nine eight seven six five four three two one ; do echo $i ; done
Note: The kubectl utility on jump_host has been configured to work with the kubernetes cluster.

```
vi job.yml
[

apiVersion: batch/v1
kind: Job
metadata:
  name: countdown-datacenter
spec:
  template:
    metadata:
      name: countdown-datacenter
    spec:
      containers:
        - name: container-countdown-datacenter
          image: ubuntu:latest
          command: ["/bin/sh", "-c"]
          args:
            [
              "for i in ten nine eight seven six five four three two one ; do echo $i ; done",
            ]
      restartPolicy: Never 
]
kubectl apply -f countdown-datacenter.yml 
```