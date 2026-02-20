# Software Requirements Specification (SRS) - AXES Project

## 1. Introduction

### 1.1 Purpose
This document provides a comprehensive overview of the AXES (Automation and XML Enhancement System) project. It outlines the functional and non-functional requirements for the platform, which serves as a centralized hub for automation quality control, report management, and remote troubleshooting.

### 1.2 Scope
The AXES system consists of:
- **Project AXES Backend**: A Node.js/Express server managing logic, database interactions, and real-time updates.
- **AXES Redux Frontend**: A React-based web dashboard for users to interact with the system.
- **Websockify**: A proxy for VNC connections enabling remote access.

### 1.3 Definitions, Acronyms, and Abbreviations
- **QC**: Quality Control
- **IPA/TPA**: Categories of QC scripts/reports.
- **IMS**: Integrated Management System (likely the target system for regression).
- **VNC**: Virtual Network Computing.
- **Sequelize**: The ORM used for database management.

---

## 2. Overall Description

### 2.1 Product Perspective
AXES is designed to streamline the automation workflow. It integrates with existing QC tools to provide a unified interface for executing scripts, viewing reports, and monitoring server health in real-time.

### 2.2 User Classes and Characteristics
- **Admins**: Manage users, project configurations, and system-wide settings.
- **QC Engineers**: Execute QC scripts, analyze reports, and monitor IMS regression status.
- **Developers**: Use the VNC proxy for remote debugging and system maintenance.

### 2.3 Operating Environment
- **Operating System**: Windows (Target), but server-side logic is cross-platform (Node.js).
- **Database**: SQL-based (configured via Sequelize).
- **Network**: Requires HTTP/S (API) and WebSockets (Real-time updates & VNC).

---

## 3. System Features

### 3.1 User Authentication
- **Description**: Secure login using JWT (JSON Web Tokens).
- **Requirements**: Middleware to verify authorization for all protected routes.

### 3.2 Report Management
- **Description**: Handling of automation reports.
- **Functional Requirements**:
    - Upload zip files containing reports.
    - Extract and host reports temporarily for viewing.
    - Archive older reports and logs according to scheduled tasks.

### 3.3 QC Execution Management
- **Description**: Orcherstration of quality control scripts.
- **Functional Requirements**:
    - Queue management for pending executions.
    - Categorization by IPA/TPA.
    - Execution history tracking and logging.

### 3.4 Real-time IMS Monitoring
- **Description**: Real-time server status updates using Socket.IO.
- **Functional Requirements**:
    - Monitor connectivity with IMS servers.
    - Broadcast status changes to all connected clients.

### 3.5 VNC Proxy
- **Description**: Remote access to servers via web-based VNC.
- **Functional Requirements**:
    - Proxy VNC traffic through Websockify.
    - Provide a web interface for remote interaction.

---

## 4. Non-functional Requirements

### 4.1 Security
- JWT-based authentication for all APIs.
- Secure handling of credentials and keys.

### 4.2 Performance
- Scheduled tasks for cleanup to maintain storage and DB performance.
- Real-time updates via WebSockets to minimize polling overhead.

### 4.3 Reliability
- Comprehensive logging using Winston.
- Error handling middleware for consistent API responses.
