# nv-tf-helm-deployment
## Terraform NV Helm deployment with parameters

## Versions

| Name | Version |
|------|---------|
| terraform | >= 0.13.0|
| terraform helm provider| ~> 1.3.2 |

## Inputs

| Name | Description | Type | Default | Required |
|------|-------------|------|---------|:--------:|
| tag | neuvector version to deploy or update | `string` | `{}` | yes |
| helm_name | helm name deployment | `string` | `{}` | no |
| ns | neuvector deployment namespace | `string` | `{}` | no |
| webui_service | NodePort/LoadBalancer ... | `string` | `[]` | yes |
| containerd | Set to true, if the container runtime is containerd | `bool` | `[]` | no |
| containerd_path | If containerd is enabled, this local containerd socket path will be used /var/run/containerd/containerd.sock	 | `string` | `[]` | no |
| scanner_replicas | # replicas of scanners | `string` | `[]` | yes |
| controller_replicas | # replicas of controllers | `string` | `[]` | yes |
| registry_username | dockerhub username | `string` | `[]` | yes |
| registry_password  | dockerhub password | `string` | `[]` | yes |


### How to deploy

1. Clone the project
2. Adjust your values in   ```terraform.tfvars.tpl```
3. Rename the file to `terraform.tfvars`
4. Deploy and Manage your deployment using terraform:
    - init your plugins  - ```terraform init```
    - plan your deployment - ```terraform plan```
    - apply the changes in your cluster ```terraform apply```

5 . if your are going to use modules, create your module file
```
module "nv-deployment" {
    source                  = "git::https://github.com/devseclabs/helm-basic-nv.git?ref=main"
    # neuvector settings
    tag="4.2.1"
    scanner_replicas = "3"
    controller_replicas = "3"
    webui_service = "LoadBalancer"

    # dockerhub settings
    registry_username   = "user"
    registry_password   = "pass"
}
```
6. export your context
```
export KUBE_CTX="demo"
export KUBE_CONFIG_PATH="~/.kube/config"
```
### Clean Up
1. destroy your deployment: ```terraform destroy```
