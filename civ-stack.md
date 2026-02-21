# Civ-Stack Server Infrastructure

A NixOS based operating system, hosting relevant software for ngos and other organisations that don’t want to rely on (american) saas products for their communication and organisational structure.

This is an opinionated stack with a built in reverse proxy with relevant pre-configured applications and the ability to extend the server with custom applications.

## Possible Application Structure
```mermaid
flowchart TB
    A(["SSO Auth Provider (Authelia)"]) --> n1["File Storage"] & n5["Communication"] & n13["Organisation"]
    n1 --> n2["OpenCloud"] & n3["Collabora"] & n4["PaperlessNGX"]
    n5 --> n6["E-Mail Server"] & n7["Matrix/Element Server with Element Call for Video Conferencing"] & n8["Outwards Communication"]
    n8 --> n9["Mastodon"] & n10["Website"] & n11["Pixelfed"] & n12["Peertube"] & n19["Newsletter (Listmonk)"]
    n13 --> n14["Calendar"] & n15["Notes (Notion Like)"] & n16["Task Management"] & n17["Password Management (Bitwarden)"] & n18["Forms (like Tally)"]

    n2@{ shape: text}
    n3@{ shape: text}
    n4@{ shape: text}
    n6@{ shape: text}
    n7@{ shape: text}
    n9@{ shape: text}
    n10@{ shape: text}
    n11@{ shape: text}
    n12@{ shape: text}
    n19@{ shape: text}
    n14@{ shape: text}
    n15@{ shape: text}
    n16@{ shape: text}
    n17@{ shape: text}
    n18@{ shape: text}
```

## Possible Architecture
```mermaid
flowchart TB

    %% =========================
    %% Physical / Virtual Layer
    %% =========================
    subgraph L0["L0 — Host Environment"]
        H1["Bare Metal Server"]
        H2["Cloud VPS"]
        H3["Virtual Machine (Proxmox / etc.)"]
    end

    %% =========================
    %% Base System Layer
    %% =========================
    subgraph L1["L1 — NixOS Base System"]
        N1["NixOS"]
        N2["Systemd"]
        N3["Firewall"]
        N4["Automatic Updates"]
        N5["Rollback Generations"]
    end

    %% =========================
    %% Civstack Core Infrastructure
    %% =========================
    subgraph L2["L2 — Civstack Core Infrastructure"]
        C1["Reverse Proxy (Caddy/Nginx)"]
        C2["SSO Provider (Authelia)"]
        C3["PostgreSQL"]
        C4["Redis"]
        C5["Mail Server"]
        C6["Backup Service (Restic)"]
        C7["Secrets Management"]
    end

    %% =========================
    %% Curated Built-in Services
    %% =========================
    subgraph L3["L3 — Curated Services (Optional Modules)"]
        S1["Matrix"]
        S2["File Storage"]
        S3["Paperless"]
        S4["Mastodon"]
        S5["PeerTube"]
        S6["Calendar / Tasks / Notes"]
    end

    %% =========================
    %% Custom Applications Layer
    %% =========================
    subgraph L4["L4 — Custom Applications"]
        A1["Medusa Backend"]
        A2["SvelteKit Frontend"]
        A3["Other Custom Apps"]
    end

    %% =========================
    %% Admin Interface
    %% =========================
    subgraph L5["L5 — Configuration Layer"]
        CFG["civstack.nix Configuration"]
    end

    %% Connections

    H1 --> N1
    H2 --> N1
    H3 --> N1

    N1 --> C1
    N1 --> C2
    N1 --> C3
    N1 --> C4
    N1 --> C5
    N1 --> C6
    N1 --> C7

    C1 --> S1
    C1 --> S2
    C1 --> S3
    C1 --> S4
    C1 --> S5
    C1 --> S6
    C1 --> A1
    C1 --> A2
    C1 --> A3

    C3 --> S1
    C3 --> S4
    C3 --> A1

    C4 --> S1
    C4 --> A1

    C6 --> C3
    C6 --> S1
    C6 --> S2
    C6 --> A1

    CFG --> N1
```
