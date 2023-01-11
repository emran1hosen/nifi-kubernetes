# Kubernetes manifest to deploys Apache NiFi 1.18 in a production environment

This configuration creates a DaemonSet named "nifi", which ensures that a single NiFi pod runs on every node in the cluster. It runs the NiFi container as non-root user using securityContext, uses init-container to chown the nifi config and data directory, uses configMap and PVC for storing configuration and data respectively, uses liveness and readiness probe to check the health of pod and also sets the limits and requests for CPU and memory resources.

This ingress configuration uses the nginx ingress controller and routes all traffic to the nifi-web-http port of the service named "nifi-service", while rewriting the path to "/nifi" to allow routing to the root of the nifi web UI. Also it is using ssl-redirect as false which means it will not redirect to https
It uses nifi.example.com as the hostname for ingress, you should replace it with your own domain or dns name for the cluster.


Please note that you may need to adjust the configurations to match your specific environment and usecase.