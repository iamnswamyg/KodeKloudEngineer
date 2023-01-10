We deployed a Nginx and PHPFPM based setup on Kubernetes cluster last week and it had been working fine. This morning one of the team members made a change somewhere which caused some issues, and it stopped working. Please look into the issue and fix it:
The pod name is nginx-phpfpm and configmap name is nginx-config. Figure out the issue and fix the same.
Once issue is fixed, copy /home/thor/index.php file from jump host into nginx-container under nginx document root and you should be able to access the website using Website button on top bar.
Note: The kubectl utility on jump_host has been configured to work with the kubernetes cluster.

```
kubectl get pods
kubectl get configmap
kubectl describe configmap nginx-config
kubectl get pod nginx-phpfpm -o yaml  > /tmp/nginx.yaml
ll /tmp/
cat /tmp/nginx.yaml
cat /tmp/nginx.yaml  |grep /usr/share/nginx/html
// Edit the nginx.yaml file and changed ‘/usr/share/nginx/html’ to ‘/var/www/html’
sed -i 's/\/usr\/share\/nginx\/html/\/var\/www\/html/g' /tmp/nginx.yaml
cat /tmp/nginx.yaml  |grep /var/www/html
kubectl replace -f /tmp/nginx.yaml --force
kubectl get pods
ll /home/thor/
kubectl cp  /home/thor/index.php  nginx-phpfpm:/var/www/html -c nginx-container
kubectl exec -it nginx-phpfpm -c nginx-container  -- curl -I  http://localhost:8099
```
