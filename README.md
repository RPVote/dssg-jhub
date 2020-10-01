# JupyterHub Configuration for DSSG2020
![Deploy](https://github.com/DSSG-eiCompare/dssg-jhub/workflows/Deploy/badge.svg)

This repository managed a JupyterHub setup for the [2020 Data Science for Social Good](https://escience.washington.edu/dssg/) program at the University of Washington eScience Institute using hubploy continuous deployment tooling:
https://github.com/yuvipanda/hubploy-template
https://github.com/yuvipanda/hubploy


### Notes

Infrastructure setup here:
https://github.com/RPVote/terraform-deploy

Default Docker environment configured here:
https://github.com/RPVote/jhub-rstudio


### tearing everything down (09/2020)
https://zero-to-jupyterhub.readthedocs.io/en/latest/setup-jupyterhub/turn-off.html
```
cd dssg/terraform-deploy/aws
helm list -A    

#NAME              	NAMESPACE       	REVISION	UPDATED                             	STATUS  	CHART                   	APP VERSION
#cluster-autoscaler	kube-system     	1       	2020-05-15 16:53:38.933289 -0700 PDT	deployed	cluster-autoscaler-7.3.1	1.17.1     
#dssg2020-prod     	dssg2020-prod   	10      	2020-07-17 12:46:49.227817 -0700 PDT	deployed	hub-0.0.1               	1.0        
#dssg2020-staging  	dssg2020-staging	24      	2020-07-17 12:30:43.60577 -0700 PDT 	deployed	hub-0.0.1               	1.0        
#efs-provisioner   	support         	1       	2020-05-15 16:53:38.943406 -0700 PDT	deployed	efs-provisioner-0.11.0  	v2.4.0   

helm delete -n support efs-provisioner
helm delete -n kube-system cluster-autoscaler
helm delete -n dssg2020-prod dssg2020-prod 
helm delete -n dssg2020-staging dssg2020-staging

kubectl delete namespace dssg2020-prod dssg2020-staging support

terraform destroy
# Plan: 0 to add, 0 to change, 58 to destroy.
```
