# Kubernetes Service Discovery

Modern cloud-native applications run as microservices using pods or containers. In these environments, microservices need to communicate dynamically without manual configuration. Service discovery makes this possible.

## What is Service Discovery?

Service discovery is a mechanism by which services discover each other dynamically without the need for hard coding IP addresses or endpoint configuration.

In modern cloud-native infrastructure such as Kubernetes, applications are designed using microservices. The different components need to communicate within a microservices architecture for applications to function, but individual IP addresses and endpoints change dynamically.

As a result, there is a need for service discovery so services can automatically discover each other.

## Types of service discovery

There are multiple different types of service discovery.

### Server-side service discovery

Server-side service discovery involves putting a load balancer (LB) in front of the service and letting the load balancer connect to service instances. This process eliminates client-side complexity. The client simply points to the IP or DNS name of the load balance.

This approach simplifies service discovery for the clients, but the LB becomes a single point of failure and bottleneck. Additionally, the LB must implement service discovery logic to point to the correct instances of pods running at any point in time

### Service registry

Another approach to service discovery is to remove the LB component and implement service discovery on the client-side using a centralized service registry

The service registry contains information about service endpoints where clients can send requests.

The main advantage of a service registry compared to a server-side approach is that there is one less component to manage (no LB) and no bottleneck.

However, the tradeoff is that a service registry complicates the client-side logic. The client must implement logic to keep the registry updated to ensure it contains the latest information about the backend pods/containers.

## Kubernetes service discovery for API-aware clients

In Kubernetes, an application deployment consists of a pod or set of pods. Those pods are ephemeral, meaning that the IP addresses and ports change constantly. This constant change makes service discovery a significant challenge in the Kubernetes world.

One way Kubernetes provides service discovery is through its endpoints API. With the endpoints API, client software can discover the IP and ports of pods in an application.

In the example below, the Kubernetes control plane ETCD acts as a service registry where all the endpoints are registered and kept up to date by Kubernetes itself. For example, a service mesh can implement logic to use an API for service discovery. That process is the native service discovery provided by Kubernetes.

## Kubernetes service discovery using service objects and kube-proxy


```sh
k -n play run -it --rm tmp-shell --restart=Never  --image=busybox -- sh
```
