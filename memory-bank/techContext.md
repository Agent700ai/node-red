# Technical Context

This document outlines the technology stack, dependencies, and integration points for the Agent700 Workflow Automation project.

## 1. Backend

### 1.1. Core Engine: Node-RED

Node-RED serves as the foundational backend for workflow execution. It is a low-code, flow-based development tool for event-driven applications, making it ideal for wiring together our agents, APIs, and other services.

-   **Version:** Node.js v18.x (LTS) is recommended.
-   **Key Role:**
    -   Provides the core engine for executing user-created workflows.
    -   Manages the state and logic of the workflow nodes.
    -   Exposes a REST API for the frontend to manage workflows (create, read, update, delete, execute).
-   **Resources:**
    -   **Official Documentation:** [https://nodered.org/docs/user-guide/](https://nodered.org/docs/user-guide/)
    -   **Community Forum:** [https://discourse.nodered.org/](https://discourse.nodered.org/)
    -   **Flow Library:** [https://flows.nodered.org/](https://flows.nodered.org/)

### 1.2. Deployment & Containerization

-   **Technology:** Docker / Kubernetes (K8s)
-   **Purpose:** The Node-RED instance will be containerized using Docker and deployed on a Kubernetes cluster. This ensures scalability, reliability, and consistent environments across development, staging, and production.

## 2. Frontend

### 2.1. Core Framework: React.js

-   **Version:** React 18.x
-   **Purpose:** The entire workflow builder UI will be a Single Page Application (SPA) built with React. It will be responsible for all user-facing interactions.

### 2.2. Workflow Canvas: React Flow

-   **Version:** Latest stable version.
-   **Purpose:** This library will be used to create the interactive, canvas-style, drag-and-drop interface for building workflows. It handles the rendering of nodes, edges, and the overall graph visualization.

### 2.3. Styling: Tailwind CSS

-   **Version:** Latest stable version.
-   **Purpose:** A utility-first CSS framework used to rapidly build and style the custom UI components, ensuring they align with Agent700's brand identity.

## 3. Authentication

-   **Provider:** WorkOS
-   **Protocol:** SAML
-   **Purpose:** WorkOS will handle user authentication for the workflow builder. All API requests from the frontend to the Node-RED backend will be authenticated to ensure that users can only access and manage their own workflows, providing enterprise-grade security.

## 4. Key External Dependencies

### 4.1. Agent700 API

-   **Endpoint:** TBD (e.g., `https://api.agent700.ai`)
-   **Critical Role:** This is the most critical integration point. The custom Node-RED nodes will interact directly with the Agent700 API to:
    -   Fetch a list of available agents for the user.
    -   Trigger agent executions.
    -   Pass data between workflow steps and agents.
    -   Retrieve results from agent operations.