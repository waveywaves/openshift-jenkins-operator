[![Docker Repository on Quay](https://quay.io/repository/redhat-developer/openshift-jenkins-operator/status "Docker Repository on Quay")](https://quay.io/repository/redhat-developer/openshift-jenkins-operator) [![Quality Gate Status](https://sonarcloud.io/api/project_badges/measure?project=akram_openshift-jenkins-operator&metric=alert_status)](https://sonarcloud.io/dashboard?id=akram_openshift-jenkins-operator)


# openshift-jenkins-operator
An operator-managed OpenShift Jenkins for OpenShift 4.x

## Requirements

## Installation

## Running Locally

To run the operator locally, you need to have your OpenShift clusters
active by running either of these commands:
``` bash
# This sets your active credentials in ~/.kube/config
oc login your-server -u your-user -p your-password
```
or
``` bash
export KUBECONFIG=/home/user/path/to/kubeconfig`
```

Then run this command to run the operator:
``` bash
make run-local
```
## Access the Jenkins web UI when Running Locally

Follow these steps to access the Jenkins web UI:

First, create the Jenkins custom resource (CR):
``` bash
oc create -f deploy/crds/jenkins_ephemeral_v1alpha1_jenkins_cr.yaml
jenkins.jenkins.dev/example-jenkins created
```
Second, identify the route to the Jenkins console:
```bash
oc get routes -o jsonpath='{range .items[*].spec}{"https://"}{.host}{end}{":443\n"}'
https://example-jenkins-jenkins-demo.apps.my-cluster.testcluster.openshift.com:443
```
And then, navigate to the route in your browser. You will be redirected
by Jenkins to log into the OpenShift console before the Jenkins console
web UI is opened.

## Creating a Pipeline

Creating a new project that defines a pipeline (for example, through a
project's JenkinsFile) will automatically create a job and build in
the Operator managed instance of Jenkins.

For example:
``` bash
oc new-app https://github.com/waveywaves/nodejs-ex --context-dir openshift/pipelines
```






