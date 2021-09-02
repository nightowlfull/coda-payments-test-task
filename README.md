# coda-payments-test-task

## Prerequisites 

- aws-cli
- Terraform


### Steps to create infrastructure using Terraform 


**Step 1:** EXPORT AWS secret credentials `AWS_ACCESS_KEY_ID` and `AWS_SECRET_ACCESS_KEY` before running `terraform init`


**Step 2:** Goto the Terraform folder and initialize terraform.
```
$ terraform init
```

**Step 3:** Shows Terraform configuration(optional).
```
$ terraform plan
```

**Step 4:** Terraform apply on infrastruture.
```
$ terraform apply
```

If we want to destory Terraform environemnt then use:
```
$ terraform destroy
```

### Create following repository secrets on github, this is required to run github action pipeline

```sh

    AWS_ACCESS_KEY_ID 

    AWS_REGION

    AWS_SECRET_ACCESS_KEY

    ECR_REGISTRY

    ECR_REPOSITORY

    KUBE_CONFIG_DATA

```

>> Find `ECR_REGISTRY` and `ECR_REPOSITORY` from AWS ECR after `terraform apply`, 

For `KUBE_CONFIG_DATA` get its value from following command 

```sh
    cat kubeconfig_coda-payment-rest-api-dev | base64
```
>> `kubeconfig_coda-payment-rest-api-dev` would be available after sucessfully infrastructure provision using `terraform apply` in terraform folder. 

## Further Improvements that can be made on EKS Cluster

1. **Ingress** : An Ingress resource could be attached to service that will make a loadbalancer available which can be used outside EKS Cluster

2. **Health Checks** : Health checks could be added to API to do health checks.

3. **Monitoring** : For monitoring, Prometheus and Grafana Dashboard could be setup that will keep monitoring the pods withing the EKS cluster and would help in understanding the CPU and Memory Usage.

4. **Logging** : For logging Loki deamonset could be run on each EKS worker node which will keep fetching logs from each container and that can be viewed through Grafana.
