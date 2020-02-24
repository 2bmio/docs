# Quotas

## Resource quotas per project

```text
# get
oc get limits -n demoproject
oc get quota -n demoproject

# describe
oc describe quota core-object-counts -n demoproject

# patch
oc patch bc/yourappname --patch '{"spec":{"resources":{"limits":{"memory":"1Gi"}}}}

https://access.redhat.com/documentation/en-us/openshift_container_platform/3.7/html/developer_guide/dev-guide-compute-resources
https://docs.openshift.com/enterprise/3.1/dev_guide/limits.html
https://docs.openshift.com/container-platform/4.3/applications/quotas/quotas-setting-per-project.html


```

