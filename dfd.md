# Data Flow Diagram (DFD) - AXES Project

## 1. Level 0: Context Diagram

The context diagram shows the interaction between the AXES system and external entities.

```mermaid
graph LR
    User((User/Client))
    AXES[AXES System]
    DB[(Database)]
    VNC_Server((VNC Server))
    IMS_Server((IMS Servers))

    User -- Requests/Commands --> AXES
    AXES -- Responses/UI --> User
    AXES -- CRUD Operations --> DB
    AXES -- Proxy VNC Traffic --> VNC_Server
    IMS_Server -- Status Updates --> AXES
```

---

## 2. Level 1: Functional Decomposition

Level 1 breaks down the AXES system into major functional processes.

```mermaid
graph TD
    User((User/Client))
    subgraph AXES_System
        P1[Authentication]
        P2[Report Management]
        P3[QC Execution Engine]
        P4[IMS Monitoring]
        P5[Websockify VNC Proxy]
    end
    
    DB[(Database)]
    FS[File System]
    IMS_Node((IMS Nodes))
    VNC_Node((Remote Desktop))

    %% Authentication Flow
    User -- Login Credentials --> P1
    P1 -- Verify User --> DB
    P1 -- JWT Token --> User

    %% Report Flow
    User -- Upload Reports --> P2
    P2 -- Extract/Store --> FS
    P2 -- Save Metadata --> DB
    P2 -- Hosted Link --> User

    %% QC Execution Flow
    User -- Trigger QC --> P3
    P3 -- Queue/Status --> DB
    P3 -- Run Scripts --> FS

    %% Monitoring Flow
    IMS_Node -- Real-time Status --> P4
    P4 -- Broadcast (Socket.IO) --> User

    %% VNC Flow
    User -- Remote Access Request --> P5
    P5 -- Redirect/Proxy --> VNC_Node
```

---

## 3. Data Stores
- **Database**: Stores `users`, `reports`, `execution_history`, `execution_queue`, `projects`, and `ims_servers_configuration`.
- **File System**: Stores physical `.zip` report files, extracted logs, and application logs.
