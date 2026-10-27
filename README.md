# Node.js Service Deployment

A simple Node.js service that returns `Hello, world!` and gets deployed to a Linux server automatically with GitHub Actions.

Project idea from [roadmap.sh](https://roadmap.sh/projects/nodejs-service-deployment).

## Run locally

```bash
npm start
```

Open http://localhost:3000

## First time server setup (Ansible)

1. Put your server IP in `ansible/inventory.ini`
2. Run:

```bash
ansible-playbook -i ansible/inventory.ini ansible/deploy.yml
```

This installs Node.js, git and pm2, clones the repo to `/opt/app` and starts the app.

## Automatic deploy (GitHub Actions)

Every push to `main` connects to the server over SSH, pulls the latest code and restarts the app with pm2.

Add these secrets in **Settings → Secrets and variables → Actions**:

| Secret | Value |
| --- | --- |
| `SERVER_HOST` | Server IP address |
| `SERVER_USER` | SSH user (e.g. `root`) |
| `SSH_PRIVATE_KEY` | Private SSH key that can log in to the server |
