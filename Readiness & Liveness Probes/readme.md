Liveness Probe

          livenessProbe:
            httpGet:
              path: /
              port: 80
            initialDelaySeconds: 5
            periodSeconds: 10


Liveness Probe checks if the container is still alive.
httpGet: Kubernetes makes an HTTP request to check if the container is responding.
path: /: Kubernetes requests the root (/) path of the Nginx server.
port: 80: The request is sent to port 80 (default Nginx port).
initialDelaySeconds: 5: Wait 5 seconds before the first check.
periodSeconds: 10: Kubernetes will check every 10 seconds.
💡 If the liveness probe fails (e.g., Nginx crashes), Kubernetes will restart the container.


Readiness Probe

          readinessProbe:
            httpGet:
              path: /
              port: 80
            initialDelaySeconds: 5
            periodSeconds: 10


Readiness Probe checks if the container is ready to serve traffic.
Works similarly to the liveness probe, but:
If the readiness probe fails, the pod is marked as "Not Ready".
The pod won't receive traffic from the Service until the probe succeeds.
💡 This prevents traffic from reaching a container that is still starting up or is temporarily overloaded.



Feature	and Purpose

Liveness Probe	Checks if the container is still running. If it fails, Kubernetes restarts the container.

Readiness Probe	Checks if the container is ready to accept traffic. If it fails, Kubernetes removes the pod from service until it recovers.