# Podman Jenkins Pipeline

This project builds and deploys the website with Podman through Jenkins.

## Jenkins host setup

Jenkins runs Podman as the `jenkins` user. Configure a subordinate UID/GID range
once on the Jenkins host before running the pipeline:

```bash
sudo usermod --add-subuids 100000-165535 jenkins
sudo usermod --add-subgids 100000-165535 jenkins
sudo loginctl enable-linger jenkins
sudo -iu jenkins podman system migrate
```

Restart Jenkins after changing these settings. Verify the setup with:

```bash
sudo -iu jenkins podman info
```

The Jenkins host must also have port `8080` available.

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
