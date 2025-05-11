# Readyness probe
A readiness probe is a Kubernetes concept used to determine whether a container in a pod is ready to accept traffic. This is part of Kubernetes' self-healing and scaling features, helping ensure that only healthy containers receive requests.

How it works:

1. Kubernetes uses the readiness probe to decide if a Pod should be part of the Service's endpoints.
2. If the probe fails, the Pod is removed from the load balancer's target list until it passes again.
3. This is different from a liveness probe, which determines if a container needs to be restarted.

# Common Readiness Probe Types:
HTTP GET:

Kubernetes sends an HTTP request to the container:
```
readinessProbe:
  httpGet:
    path: /health
    port: 8080
  initialDelaySeconds: 5
  periodSeconds: 10
```
TCP Socket:

Kubernetes attempts to open a socket on the specified port:
```
readinessProbe:
  tcpSocket:
    port: 8080
  initialDelaySeconds: 5
  periodSeconds: 10
```
# Liveness probe
  A liveness probe in Kubernetes is used to check whether a container is still running properly. If the liveness probe fails, Kubernetes will restart the container, assuming it's in a bad state and can't recover on its own.

# Common Liveness Probe Types:
HTTP GET:
```
livenessProbe:
  httpGet:
    path: /health
    port: 8080
  initialDelaySeconds: 10
  periodSeconds: 10
```
TCP Socket:
```
livenessProbe:
  tcpSocket:
    port: 8080
  initialDelaySeconds: 10
  periodSeconds: 10
```
# Init Containers
  Init containers in Kubernetes are special containers that run before the main application containers in a Pod start. They're used for initialization tasks like setting up dependencies, configurations, or performing checks.

Key Features:

1. Run sequentially, one after another.
2. Each must succeed before the next starts.
3. If any init container fails, Kubernetes will restart the pod (based on its restart policy).

Common Use Cases:

1. Waiting for a service to become available (e.g., wait for a DB to be ready).
2. Setting up configuration files or secrets.
3. Data migrations or pre-processing before the app runs.
4. Populating volumes shared with the main container.

# Use of configmap as volume
An application has mainly two segments one is application code and another is configuration,if code updated then image building is nessessary but coming to configuration we reduce one step by configuring configmap(no need to build image)

steps to create:
consider expense project frontend nginx has configuration
1. create a configmap for nginx configuration
2. refer in pod definition 
3. create volume mounts 