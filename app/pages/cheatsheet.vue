<script setup>
const containerManagement = [
  { command: "docker run", description: "Create & start" },
  { command: "docker run -d", description: "Detached mode" },
  { command: "docker run -it", description: "Interactive mode" },
  { command: "docker run --name", description: "Assign name" },
  { command: "docker run -p", description: "Map port" },
  { command: "docker run -v", description: "Mount volume" },
  { command: "docker run --rm", description: "Auto-remove" },
  { command: "docker run -e", description: "Set env var" },
  { command: "docker run --network", description: "Set network" },
  { command: "docker ps", description: "Running containers" },
  { command: "docker ps -a", description: "All containers" },
  { command: "docker stop", description: "Graceful stop" },
  { command: "docker kill", description: "Force stop" },
  { command: "docker start", description: "Start container" },
  { command: "docker restart", description: "Restart container" },
  { command: "docker rm", description: "Remove stopped" },
  { command: "docker rm -f", description: "Force remove" },
  { command: "docker exec -it", description: "Open shell" },
  { command: "docker logs", description: "Fetch logs" },
  { command: "docker logs -f", description: "Follow logs" },
  { command: "docker inspect", description: "JSON details" },
  { command: "docker cp", description: "Copy files" },
  { command: "docker rename", description: "Rename container" },
]

const imageManagement = [
  { command: "docker images", description: "List images" },
  { command: "docker pull", description: "Download image" },
  { command: "docker push", description: "Upload image" },
  { command: "docker build -t", description: "Build image" },
  { command: "docker build --no-cache", description: "Build no cache" },
  { command: "docker rmi", description: "Remove image" },
  { command: "docker rmi -f", description: "Force remove" },
  { command: "docker tag", description: "Tag image" },
  { command: "docker history", description: "Layer history" },
  { command: "docker inspect", description: "Image metadata" },
  { command: "docker save -o", description: "Export tar" },
  { command: "docker load -i", description: "Import tar" },
  { command: "docker image prune", description: "Remove dangling" },
]

const systemCommands = [
  { command: "docker info", description: "System info" },
  { command: "docker version", description: "Client & daemon" },
  { command: "docker system prune", description: "Remove unused" },
  { command: "docker system df", description: "Disk usage" },
]

const volumeNetwork = [
  { command: "docker volume create", description: "Create volume" },
  { command: "docker volume ls", description: "List volumes" },
  { command: "docker volume inspect", description: "Volume details" },
  { command: "docker volume rm", description: "Remove volume" },
  { command: "docker volume prune", description: "Remove unused" },
  { command: "docker network create", description: "Create network" },
  { command: "docker network ls", description: "List networks" },
  { command: "docker network inspect", description: "Network details" },
  { command: "docker network connect", description: "Connect container" },
  { command: "docker network disconnect", description: "Disconnect container" },
  { command: "docker network rm", description: "Remove network" },
]

const containerLifecycle = [
  { command: "docker create", description: "Create only" },
  { command: "docker start", description: "Start container" },
  { command: "docker pause", description: "Pause processes" },
  { command: "docker unpause", description: "Resume container" },
  { command: "docker stop", description: "Graceful stop" },
  { command: "docker kill", description: "Force kill" },
  { command: "docker wait", description: "Wait exit code" },
  { command: "docker rm", description: "Remove stopped" },
  { command: "docker commit", description: "Snapshot image" },
]

const dockerComposeCode = `version: '3.8'
services:
  web:
    image: nginx:alpine
    ports:
      - "80:80"
    volumes:
      - ./html:/usr/share/nginx/html
    depends_on:
      - db

  db:
    image: postgres:15
    environment:
      POSTGRES_USER: user
      POSTGRES_PASSWORD: secret
      POSTGRES_DB: mydb
    volumes:
      - db_data:/var/lib/postgresql/data

volumes:
  db_data:`

const registryOperations = [
  { command: "docker login", description: "Authenticate registry" },
  { command: "docker logout", description: "Log out" },
  { command: "docker search", description: "Search Hub" },
]

const dockerSecrets = [
  { command: "docker secret create", description: "Create secret" },
  { command: "docker secret ls", description: "List secrets" },
]

const advancedTips = [
  { description: "Use multi-stage builds to keep final images small by separating build and runtime layers." },
  { description: "Order Dockerfile instructions from least to most frequently changed to maximise layer cache reuse." },
  { description: "Prefer COPY over ADD unless you need automatic tar extraction or remote URL fetching." },
  { description: "Use .dockerignore to exclude node_modules, .git, and build artifacts from the build context." },
  { description: "Pin base image versions (e.g. node:20-alpine) to ensure reproducible builds across environments." },
  { description: "Run containers as a non-root user with the USER instruction to reduce attack surface." },
]

const dockerOperations = [
  { command: "docker stats", description: "Resource usage" },
  { command: "docker top", description: "Running processes" },
]

const configFiles = [
  { command: "~/.docker/config.json", description: "CLI config" },
  { command: "/etc/docker/daemon.json", description: "Daemon config" },
  { command: "docker config create", description: "Create config" },
  { command: "docker config ls", description: "List configs" },
]
</script>


<template>
  <div class="min-h-screen bg-white">
    <AppHeader />

    <div class="pt-16 max-w-7xl mx-auto px-6 flex">
      <div class="w-full">
        <div class="flex items-center justify-center gap-3 py-4">
          <img src="/dockeLogo.webp" alt="Docker" class="w-20 h-20 object-contain" />
          <span
            class="font-bold text-5xl"
            style="color: #0d3b69; text-shadow: 0 0 6px #7dd3fc, 0 0 14px #38bdf8;"
          >DOCKER</span>
        </div>
        <div>
          <CommandsCard :commands="containerManagement" title="Container Management" />
          <CommandsCard :commands="imageManagement" title="Image Management" />
          <CommandsCard :commands="systemCommands" title="System Commands" />
          <CommandsCard :commands="volumeNetwork" title="Volume & Network" />
          <CommandsCard :commands="containerLifecycle" title="Container Lifecycle" />
          <CommandsCard type="code" :codeBlock="dockerComposeCode" title="Docker Compose" />
          <CommandsCard :commands="registryOperations" title="Registry Operations" />
          <CommandsCard :commands="dockerSecrets" title="Docker Secrets" />
          <CommandsCard :commands="advancedTips" type="tips" title="Advanced Tips & Optimization" />
          <CommandsCard :commands="dockerOperations" title="Docker Operations" />
          <CommandsCard :commands="configFiles" title="Config Files" />
        </div>

      </div>
      <div>Heyy ZZZ</div>
    </div>
  </div>
</template>
