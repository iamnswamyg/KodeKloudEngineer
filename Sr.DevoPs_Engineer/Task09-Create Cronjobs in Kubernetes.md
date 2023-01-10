There are some jobs/tasks that need to be run regularly on different schedules. Currently the Nautilus DevOps team is working on developing some scripts that will be executed on different schedules, but for the time being the team is creating some cron jobs in Kubernetes cluster with some dummy commands (which will be replaced by original scripts later). Create a cronjob as per details given below:
1.Create a cronjob named datacenter.
2.Set schedule to */12 * * * *.
3.Container name should be cron-datacenter.
4.Use nginx image with latest tag only and remember to mention the tag i.e nginx:latest.
5.Run a dummy command echo Welcome to xfusioncorp!.
6.Ensure restart policy is OnFailure.
Note: The kubectl utility on jump_host has been configured to work with the kubernetes cluster.

```
kubectl get pod
kubectl get cronjob
vi /tmp/cron.yml
[
apiVersion: batch/v1beta1
kind: CronJob
metadata:
  name: datacenter
spec:
  schedule: "*/12 * * * *"
  jobTemplate:
    spec:
      template:
        spec:
          containers:
          - name: cron-datacenter
            image: nginx:latest
            args:
            - /bin/sh
            - -c
            - echo Welcome to xfusioncorp!
          restartPolicy: OnFailure

]
kubectl create -f /tmp/cron.yml
kubectl get cronjob
kubectl get pod
kubectl logs datacenter-1673024280-55v47
```