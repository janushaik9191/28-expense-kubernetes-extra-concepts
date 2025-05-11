# Readyness probe
A readiness probe is a Kubernetes concept used to determine whether a container in a pod is ready to accept traffic. This is part of Kubernetes' self-healing and scaling features, helping ensure that only healthy containers receive requests.

How it works:
Kubernetes uses the readiness probe to decide if a Pod should be part of the Service's endpoints.

If the probe fails, the Pod is removed from the load balancer's target list until it passes again.

This is different from a liveness probe, which determines if a container needs to be restarted.

# Common Readiness Probe Types:
HTTP GET
Kubernetes sends an HTTP request to the container:

readinessProbe:
  httpGet:
    path: /health
    port: 8080
  initialDelaySeconds: 5
  periodSeconds: 10

TCP Socket
Kubernetes attempts to open a socket on the specified port:

readinessProbe:
  tcpSocket:
    port: 8080
  initialDelaySeconds: 5
  periodSeconds: 10

# Liveness probe
  A liveness probe in Kubernetes is used to check whether a container is still running properly. If the liveness probe fails, Kubernetes will restart the container, assuming it's in a bad state and can't recover on its own.

# Common Liveness Probe Types:
HTTP GET

livenessProbe:
  httpGet:
    path: /health
    port: 8080
  initialDelaySeconds: 10
  periodSeconds: 10

TCP Socket

livenessProbe:
  tcpSocket:
    port: 8080
  initialDelaySeconds: 10
  periodSeconds: 10

# Init Containers
  Init containers in Kubernetes are special containers that run before the main application containers in a Pod start. They're used for initialization tasks like setting up dependencies, configurations, or performing checks.

# Key Features:

Run sequentially, one after another.

Each must succeed before the next starts.

If any init container fails, Kubernetes will restart the pod (based on its restart policy).

# Common Use Cases:
Waiting for a service to become available (e.g., wait for a DB to be ready).

Setting up configuration files or secrets.

Data migrations or pre-processing before the app runs.

Populating volumes shared with the main container.

