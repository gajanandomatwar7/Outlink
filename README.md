# OutLink

**OutLink** is a lightweight tunneling tool that provides secure external access to services running inside private networks and virtual machines.

It allows applications and services that are not directly reachable from the public internet to be accessed through a public endpoint, without requiring the private VM to have a public IP address.

## What OutLink Provides

* **Private-to-Public Connectivity**
  Make services running inside private VMs accessible from the internet.

* **Secure Tunneling**
  Establish an outbound tunnel from the private environment to a publicly reachable server.

* **Service Exposure**
  Expose web applications, APIs, development servers, and other TCP-based services through the tunnel.

* **Custom Domains**
  Services can be accessed using a configured domain or subdomain instead of directly exposing private IP addresses.

* **SSH Access**
  Provide external SSH access to private virtual machines through the tunneling infrastructure.

* **No Public IP Required**
  Private VMs do not need their own public IP address to receive external connections.

* **Centralized Access Point**
  Public traffic is handled through a central gateway while the actual service remains inside the private network.

## How It Works

OutLink follows a simple reverse-tunneling model:

```text
                 Internet
                    │
                    ▼
          ┌──────────────────┐
          │   OutLink Server │
          │   Public Gateway │
          └────────┬─────────┘
                   │
             Encrypted Tunnel
                   │
                   ▼
          ┌──────────────────┐
          │  Private VM      │
          │                  │
          │  Application     │
          │  API / SSH       │
          └──────────────────┘
```

The private VM establishes an outbound connection to the OutLink server. Incoming requests received by the public gateway are then forwarded through the established tunnel to the required service inside the private network.

Because the connection is initiated from the private environment, the service does not need to be directly exposed to the public internet.

## Example

A web application is running inside a private VM:

```text
Private VM
10.x.x.x:8000
```

OutLink creates a tunnel between the VM and the public gateway:

```text
Internet
   │
   ▼
app.example.com
   │
   ▼
OutLink Gateway
   │
   ▼
Private VM
10.x.x.x:8000
```

Users can access the application through the public endpoint while the application itself remains inside the private network.

## Use Cases

### Web Applications

Expose development or production web applications running inside private VMs.

### APIs

Provide external access to APIs without assigning a public IP directly to the API server.

### SSH

Allow administrators or users to connect to private VMs remotely.

### Development

Quickly make locally or privately hosted services reachable from external systems.

### Private Cloud Infrastructure

Provide internet-facing access to workloads running inside a private cloud environment.

## Key Characteristics

| Feature                   | OutLink |
| ------------------------- | ------- |
| Private VM support        | ✓       |
| Public IP required on VM  | No      |
| Reverse tunneling         | ✓       |
| Web service exposure      | ✓       |
| API exposure              | ✓       |
| SSH access                | ✓       |
| Custom domains            | ✓       |
| Centralized gateway       | ✓       |
| Private network preserved | ✓       |

## OutLink in a Private Cloud

OutLink can act as the networking layer between workloads running in a private cloud and users on the public internet.

```text
                         Internet
                            │
                            ▼
                    ┌───────────────┐
                    │    OutLink    │
                    │ Public Gateway│
                    └───────┬───────┘
                            │
                    Tunnel Connection
                            │
             ┌──────────────┴──────────────┐
             │                             │
       ┌─────▼─────┐                 ┌─────▼─────┐
       │    VM 1   │                 │    VM 2   │
       │   Web App │                 │    API    │
       └───────────┘                 └───────────┘
```

This allows private-cloud workloads to remain on private networks while still providing controlled external connectivity.

## Design Goals

OutLink is designed around four main goals:

1. **Simplicity** — expose a service without complicated network configuration.
2. **Security** — keep private workloads away from direct public exposure.
3. **Connectivity** — provide reliable access to services behind private networks.
4. **Isolation** — keep the underlying VM and private network separate from public traffic.

## Project Status

OutLink is being developed as a tunneling and service-exposure layer for private infrastructure and cloud environments.

---

**OutLink — Connect private services to the outside world.**
