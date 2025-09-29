⚙️ John's Digital Proving Ground: A Home Lab ExplorationWelcome to my home lab! This is more than just a collection of servers; it's a living, breathing production environment dedicated to continuous learning, security research, and solving real-world problems with modern IT and DevOps principles.filozofia (Philosophy)My approach to this lab is guided by three core principles:Business Continuity First: The network must be 100% stable and secure for critical tasks, like supporting my wife's remote work. Uptime is not optional.Security by Design: The architecture is built on a multi-layered, zero-trust model, from network segmentation to application identity management.Automate Everything: If a task has to be done more than once, it should be automated. The goal is a resilient, repeatable, and easily managed infrastructure.🏛️ High-Level ArchitectureThis diagram illustrates the flow of traffic and the core security layers of the lab. All external traffic is proxied through Cloudflare, with Traefik managing ingress and Authentik handling identity and authorization before a user can even reach a service.graph TD
    subgraph Internet
        A[External User]
    end

    subgraph "Cloudflare (Proxy & DNS)"
        B(johnwilson.tech)
    end

    subgraph "Home Network (Ubiquiti)"
        C{Traefik Reverse Proxy}
    end
    
    subgraph "Security Layer"
        D[Authentik IAM/SSO]
    end

    subgraph "Proxmox VE Cluster"
        E[VMs & Containers]
        F[Internal Services]
        G[Databases]
    end

    A --> B
    B --> C
    C -- Forward Auth --> D
    D -- Authenticated --> C
    C --> E
    C --> F
    C --> G
