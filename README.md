# VS Code Server on Kubernetes

This repository contains Kubernetes manifests to deploy VS Code Server (code-server) on Kubernetes with browser access.

## Components

- **Deployment**: Runs the code-server container
- **Service**: Exposes the code-server deployment
- **PersistentVolumeClaim**: Provides persistent storage for user data
- **Secret**: Stores the password for authentication
- **Ingress**: Enables browser access through a domain name

## Deployment Instructions

1. Clone this repository:
   ```
   git clone https://github.com/Shasha0072/vscode-k8s-browser-access.git
   cd vscode-k8s-browser-access
   ```

2. Modify the configuration as needed:
   - Update the password in `code-server-secret.yaml`
   - Change the domain in `code-server-ingress.yaml`
   - Adjust resource limits in `code-server-deployment.yaml`

3. Apply the Kubernetes manifests:
   ```
   kubectl apply -f code-server-pvc.yaml
   kubectl apply -f code-server-secret.yaml
   kubectl apply -f code-server-deployment.yaml
   kubectl apply -f code-server-service.yaml
   kubectl apply -f code-server-ingress.yaml
   ```

4. Access VS Code in your browser:
   ```
   https://vscode.example.com
   ```

## Multi-User Setup

For a multi-user setup, you can:

1. Create multiple deployments with different names
2. Use namespaces to isolate user environments
3. Create separate ingress rules for each user (e.g., user1.vscode.example.com)

## Security Considerations

- Change the default password in the secret
- Consider using HTTPS with proper TLS certificates
- Implement network policies to restrict access
- Use authentication at the ingress level for additional security

## Customization

You can customize the deployment by:

- Mounting additional volumes for source code
- Pre-installing extensions using custom container images
- Configuring resource limits based on your needs

## Troubleshooting

If you encounter issues:

1. Check pod status: `kubectl get pods`
2. View pod logs: `kubectl logs <pod-name>`
3. Ensure PVC is properly bound: `kubectl get pvc`
4. Verify ingress configuration: `kubectl get ingress`