# Chicken Disease Classification 🐔

A deep learning project for chicken disease classification using Convolutional Neural Networks (CNNs), with DVC for pipeline management and CI/CD deployment using GitHub Actions, Docker, AWS, and Microsoft Azure.

## 📌 Project Workflows

1. Update `config.yaml`.
2. Update `secrets.yaml` (optional).
3. Update `params.yaml`.
4. Update the entities.
5. Update the configuration manager in `src/config`.
6. Update the components.
7. Update the pipeline.
8. Update `main.py`.
9. Update `dvc.yaml`.

## 🛠️ Technologies Used

* Python
* TensorFlow / Keras
* Convolutional Neural Networks (CNNs)
* DVC (Data Version Control)
* Docker
* GitHub Actions
* AWS (ECR, EC2, IAM)
* Azure Container Registry (ACR)
* Azure Web Apps

## 🚀 Getting Started

### Prerequisites

* Python 3.8
* Git
* Conda (optional)
* Docker
* DVC

### Step 1: Clone the Repository

```bash
git clone https://github.com/mbadrawy1/Disease-Classification.git
cd Disease-Classification
```

### Step 2: Create and Activate a Conda Environment

```bash
conda create -n cnncls python=3.8 -y
conda activate cnncls
```

### Step 3: Install Dependencies

```bash
pip install -r requirements.txt
```

### Step 4: Run the Application

```bash
python app.py
```

Open the local URL displayed in your terminal to access the application.

## 🔄 DVC Commands

Initialize DVC if it has not already been initialized:

```bash
dvc init
```

Reproduce the machine learning pipeline:

```bash
dvc repro
```

Visualize the pipeline:

```bash
dvc dag
```

## ☁️ AWS CI/CD Deployment with GitHub Actions

This workflow builds a Docker image, pushes it to Amazon ECR, and deploys it to an EC2 instance.

### Deployment Workflow

1. Build a Docker image from the source code.
2. Push the image to Amazon Elastic Container Registry (ECR).
3. Launch an Ubuntu EC2 instance.
4. Configure EC2 as a self-hosted GitHub Actions runner.
5. Pull the Docker image from ECR.
6. Run the container on EC2.

### Step 1: Configure AWS IAM

Create an IAM identity for deployment with the minimum permissions required to access ECR and manage EC2 resources.

### Step 2: Create an ECR Repository

Create an Amazon ECR repository named `chicken`.

Copy your repository URI. Its format is:

```text
<AWS_ACCOUNT_ID>.dkr.ecr.<AWS_REGION>.amazonaws.com/chicken
```

### Step 3: Launch an EC2 Instance

Launch an Ubuntu EC2 instance and install Docker:

```bash
sudo apt-get update -y
sudo apt-get upgrade -y

curl -fsSL https://get.docker.com -o get-docker.sh
sudo sh get-docker.sh

sudo usermod -aG docker ubuntu
newgrp docker
```

Verify the installation:

```bash
docker --version
```

### Step 4: Configure a GitHub Actions Runner

1. Open your repository on GitHub.
2. Navigate to **Settings → Actions → Runners**.
3. Click **New self-hosted runner**.
4. Select Linux and follow the instructions to configure the runner on EC2.

### Step 5: Configure GitHub Actions Secrets

Navigate to **Settings → Secrets and variables → Actions** and configure:

| Secret                  | Description           |
| ----------------------- | --------------------- |
| `AWS_ACCESS_KEY_ID`     | AWS IAM access key    |
| `AWS_SECRET_ACCESS_KEY` | AWS IAM secret key    |
| `AWS_REGION`            | Your AWS region       |
| `AWS_ECR_LOGIN_URI`     | Your ECR registry URI |
| `ECR_REPOSITORY_NAME`   | `chicken`             |

Use GitHub OIDC and temporary credentials where possible instead of long-lived access keys.

## 🐳 Azure CI/CD Deployment with GitHub Actions

This workflow builds a Docker image, pushes it to Azure Container Registry (ACR), and deploys it to Azure Web Apps.

### Step 1: Configure Azure Container Registry

Create an Azure Container Registry and copy its login server.

Example format:

```text
<REGISTRY_NAME>.azurecr.io
```

### Step 2: Build the Docker Image

Run this command from the directory containing your `Dockerfile`:

```bash
docker build -t <REGISTRY_NAME>.azurecr.io/chicken:latest .
```

### Step 3: Log In to ACR

```bash
docker login <REGISTRY_NAME>.azurecr.io
```

Use your registry credentials or an approved secure authentication method.

### Step 4: Push the Docker Image

```bash
docker push <REGISTRY_NAME>.azurecr.io/chicken:latest
```

### Step 5: Deploy to Azure Web Apps

1. Create an Azure Web App configured for containers.
2. Configure it to use your ACR image.
3. Configure secure registry authentication.
4. Set the required application port and environment variables.
5. Restart the Web App and verify the deployment.

## 🔐 Security Best Practices

* Never commit passwords, access keys, or tokens to GitHub.
* Store secrets in GitHub Actions Secrets or use secure identity-based authentication.
* Rotate any credentials that have been exposed.
* Add sensitive files such as `.env` and `secrets.yaml` to `.gitignore`.
* Follow the principle of least privilege for cloud permissions.
* Use versioned Docker image tags for reliable deployments.

## 📁 Project Structure

The following is an example structure. Adjust it to match the actual repository.

```text
Disease-Classification/
├── config/
├── research/
├── src/
│   ├── config/
│   ├── components/
│   ├── entity/
│   └── pipeline/
├── app.py
├── main.py
├── params.yaml
├── config.yaml
├── dvc.yaml
├── requirements.txt
├── Dockerfile
└── README.md
```

## 🎯 Project Goals

* Develop a CNN-based chicken disease classification application.
* Organize the ML workflow into reusable components.
* Track and reproduce machine learning pipelines with DVC.
* Containerize the application with Docker.
* Automate deployment with GitHub Actions.
* Deploy the application using AWS and Azure services.

## 📄 License

Refer to the repository's license file for licensing information.
