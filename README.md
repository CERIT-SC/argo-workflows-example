# Argo Workflows Demo

This repository provides a basic demonstration of setting up [Argo Workflows](https://argoproj.github.io/argo-workflows/) on a managed Kubernetes cluster.

## Overview

The project includes:

- Controller manifests for deploying the Argo Workflow controller.
- Example RBAC configuration.
- A simple "Hello World" workflow to test the setup.

This demo is minimal and intended for learning and experimentation purposes. It does not include persistent storage, UI dashboard, artifact repositories, or advanced configuration.

## Setup Instructions

### 1. Deploy the Argo Workflow Controller

Apply the manifests located in the `controller-manifests` directory:

```
kubectl apply -f controller-manifests/
```

> **Note:** You may want to modify the `workflow-controller-configmap.yaml` file to fit your specific requirements. The provided configuration only sets the required `securityContext`.

### 2. Set Up RBAC for Workflow Execution

The `runner-rbac.yaml` file creates a service account along with the necessary `Role` and `RoleBinding` to allow workflow execution:

```
kubectl apply -f runner-rbac.yaml -n [your-namespace]
```

Ensure that the service account name defined here matches the one referenced in your workflows. Adjust RBAC rules as needed for your use case.

### 3. Deploy the Example Workflow

Once the controller and RBAC setup are complete, you can deploy the example "Hello World" workflow found in the `example/` folder:

```
kubectl create -f example/hello-world.yaml -n [your-namespace]
```

## Folder Structure

```
.
├── controller-manifests/      # Argo Workflow controller configuration
└── example/
    ├── runner-rbac.yaml       # Service account and RBAC setup
    └── hello-world.yaml       # Sample workflow definition
```

## Resources

- [Argo Workflows Documentation](https://argoproj.github.io/argo-workflows/)
- [Argo GitHub Repository](https://github.com/argoproj/argo-workflows)

## License

This project is licensed under the MIT License.

