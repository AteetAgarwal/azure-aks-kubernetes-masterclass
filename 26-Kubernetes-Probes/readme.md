Use below command to generate the yaml -
kubectl create deploy livenessprobe --image busybox -o yaml --dry-run
-------------------------------------

Probes Types:

Liveness probe: 
It is used to continue checking the availability of a Pod. Kubectl watches over your containers. If a container process crashes, kubelet will take care of it based on the restart policy. But this is not always enough. Your process may not crash, but instead run into an infinite loop or a deadlock. The restart policy might not be nuanced enough. With a liveness probe, you get to decide when a container is considered alive.

Kubernetes uses the liveness probe to decide when a container needs to be killed and when another instance should be launched instead. Since Kubernetes operates at a pod level, the respective pod is killed if at least one of its containers reports as being unhealthy

If a liveness probe fails for any container, then the pod's restart policy goes into effect. Make sure your restart policy is not Never, because that will make the probe useless.


Readiness Probe: 
used to make sure a Pod is not published as available, until the readinessProbe has been able to access it.
Kubernetes uses a readiness probe to decide when a service instance, that is, a container, is ready to accept traffic. Pods that are not ready (a Pod is ready only if all of its containers are considered ready) will be removed from the Service Endpoints list until they become ready again. In other words, it is a signal for notifying that a given Pod can be used for requests incoming to the Service.


Startup Probe: 
If we define a startup probe for a container, then Kubernetes does not execute the liveness or readiness probes, as long as the container's startup probe does not succeed.
Startup probes have been introduced in Kubernetes 1.16 to support cases when a container may require more time for initialization than initialDelaySeconds + failureThreshold * periodSeconds set in the readiness probe. In general, you should use the same handler configuration for startup probes that you would for readiness probes but use larger delays. If a container is not ready within initialDelaySeconds + failureThreshold * periodSeconds for a readiness probe, then the container will be killed and subject to the Pod's restart policy.

If we define a startup probe for a container, then Kubernetes does not execute the liveness or readiness probes, as long as the container's startup probe does not succeed. Once again, Kubernetes looks at pods and starts executing liveness and readiness probes on its containers if the startup probes of all the pod's containers succeed.
---------------------------------------

initialDelaySeconds: Number of seconds after the container has started before liveness or readiness probes are initiated. Defaults to 0 seconds. Minimum value is 0.

periodSeconds: How often (in seconds) to perform the probe. Default to 10 seconds. Minimum value is 1.

timeoutSeconds: Number of seconds after which the probe times out. Defaults to 1 second. Minimum value is 1.

successThreshold: Minimum consecutive successes for the probe to be considered successful after having failed. Defaults to 1. Must be 1 for liveness and startup Probes. Minimum value is 1.

failureThreshold: When a probe fails, Kubernetes will try failureThreshold times before giving up. Giving up in case of liveness probe means restarting the container. In case of readiness probe the Pod will be marked Unready. Defaults to 3. Minimum value is 1.
---------------------------------------
