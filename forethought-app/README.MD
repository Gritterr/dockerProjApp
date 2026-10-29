## Deploy the nodejs application manually
Clone the repository and build a docker image from it using following commands. This assumes that you're using an Ubuntu operating system.

```
sudo apt-get update
sudo apt-get install \
    apt-transport-https \
    ca-certificates \
    curl \
    gnupg-agent \
    software-properties-common -y
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
sudo add-apt-repository \
   "deb [arch=amd64] https://download.docker.com/linux/ubuntu \
   $(lsb_release -cs) \
   stable"
sudo apt-get update
sudo apt-get install -y docker-ce


git clone https://github.com/npsoni88/devops-monitoring.git

cd devops-monitoring/forethought-app
docker build . -t IMAGE-NAME (replace image name with your name)
docker run -d --name my-container -p 80:8080 IMAGE-NAME (replace image name with your name)

```

## Docker image

The [Dockerfile](Dockerfile) builds a small image on `node:20-alpine`: it installs the locked dependencies with `npm ci`, runs as the non-root `node` user, and has a `HEALTHCHECK` on the home page. The image is published as `saviochristopher/forethought-todo`.

```
git clone https://github.com/Gritterr/dockerProjApp.git
cd dockerProjApp/forethought-app
docker build -t saviochristopher/forethought-todo:1.0 .
docker run -d --name todo -p 8095:8080 saviochristopher/forethought-todo:1.0
```

The app keeps its tasks in memory, so it needs no volume. Each replica of a scaled service has its own list.
