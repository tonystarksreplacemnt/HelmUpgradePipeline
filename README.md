# HelmUpgradePipeline
HelmUpgradePipeline
```
name: Helm Upgrade Loki

on:
  push:
    branches:
      - main  # Change this to your main branch name if needed

jobs:
  deploy:
    runs-on: ubuntu-latest

    steps:
    - name: Checkout code
      uses: actions/checkout@v2

    - name: Set up kubectl
      uses: azure/k8s-set-context@v1
      with:
        kubeconfig: ${{ secrets.KUBE_CONFIG_DATA }}

    - name: Configure AWS credentials
      uses: aws-actions/configure-aws-credentials@v1
      with:
        aws-access-key-id: ${{ secrets.AWS_ACCESS_KEY_ID }}
        aws-secret-access-key: ${{ secrets.AWS_SECRET_ACCESS_KEY }}
        aws-region: us-east-1  # Replace with your AWS region

    - name: Helm Upgrade Loki
      run: |
        helm upgrade loki-release path/to/your/loki-chart-directory \
          --namespace loki \
          -f path/to/your/loki/values.yaml  # Adjust to the path of your values file
          --version <desired_version>  # Replace with the desired version
          --set key=value  # Specify any additional values as needed
```
