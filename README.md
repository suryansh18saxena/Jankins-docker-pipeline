# Podman Jenkins Pipeline

This project builds and deploys the website with Podman through Jenkins.

## Run locally

```bash
podman build -t myapp:latest .
podman run -d --name myapp-container -p 8080:80 myapp:latest
```

Open `http://localhost:8080`.

To stop and remove the container:

```bash
podman stop myapp-container
podman rm myapp-container
```
