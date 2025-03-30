# Azure Cloud  
Create Grafana Cloud Account which is valid for 1 Year  

Search on Google

    azure cloud free trial

# 1. Create AKS Cluster:   
Create as per described in Video:

# 2. Run the Application to test the cluster

    kubectl apply -f petclinic.yaml

# 3. Install Prometheus Node Exporter on Minikube Cluster

    helm repo add prometheus-community https://prometheus-community.github.io/helm-charts 
    helm repo update
    helm install node-exporter prometheus-community/prometheus-node-exporter

# 4. Configure and Run Alloy on Minikube Cluster

Make sure to update the node_exporter service ip in alloy configuration in configmap.alloy file before creating configmap

    kubectl create configmap --namespace metrics alloy-config "--from-file=config_k8s_metrics.alloy=./config_k8s_metrics.alloy"

    helm  upgrade --install --namespace metrics alloy grafana/alloy -f alloy_k8s_app_monitoring.yaml

# 5. Validate the metrics on Grafana
To Search all of the time series data points grouping by job  in query  

    count({__name__=~".+"}) by (job)
