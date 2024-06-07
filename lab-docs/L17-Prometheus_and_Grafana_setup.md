# Prometheus setup
### pre-requisites
1. Kubernetes cluster
2. helm

## Setup Prometheus

1. Create a dedicated namespace for prometheus 
   ```sh
   kubectl create namespace monitoring
   ```

2. Add Prometheus helm chart repository
   ```sh
   helm repo add prometheus-community https://prometheus-community.github.io/helm-charts 
   ```

3. Update the helm chart repository
   ```sh
   helm repo update
   helm repo list
   ```

4. Install the prometheus from premotheus stack, grafana also installed.

   ```sh
    helm install prometheus prometheus-community/kube-prometheus-stack --namespace monitoring
    helm pull prometheus-community/kube-prometheus-stack
   ```

5. Above helm create all services as ClusterIP. To access Prometheus out side of the cluster, we should change the service type load balancer
   ```sh 
   kubectl edit svc prometheus-kube-prometheus-prometheus -n monitoring
   # change into NodePort/loadbalancer
   
   ```
6. Loginto Prometheus dashboard to monitor application
   https://ELB:9090 or https://nodeport_ip:9090
   query: machine_cpu_cores

8. Check for node_load15 executor to check cluster monitoring 

9. We check similar graphs in the Grafana dashboard itself. for that, we should change the service type of Grafana to LoadBalancer
   ```sh 
   kubectl edit svc prometheus-grafana -n monitoring
   # shift + g : will go to end, change type to LB/NP 
   ```

10.  To login to Grafana account, use the below username and password 
    ```sh
    username: admin
    password: prom-operator
    ```
11. Here we should check for "Node Exporter/USE method/Node" and "Node Exporter/USE method/Cluster"
    USE - Utilization, Saturation, Errors
    home -> dashboard -> search kubernetes API Server
    search -> kubernetes compute services
   
13. Even we can check the behavior of each pod, node, and cluster 
