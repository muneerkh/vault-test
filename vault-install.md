https://developer.hashicorp.com/vault/docs/deploy/kubernetes/helm/openshift

https://developer.hashicorp.com/vault/tutorials/kubernetes-platforms/kubernetes-openshift


https://developer.hashicorp.com/vault/tutorials/kubernetes/kubernetes-sidecar

helm repo add hashicorp https://helm.releases.hashicorp.com

helm search repo hashicorp/vault


helm install vault hashicorp/vault \
    --create-namespace \
    --namespace vault \
    --set "global.openshift=true" \
    --set "server.dev.enabled=true"

or

helm install vault hashicorp/vault \
    --set "global.openshift=true" \
    --set "server.dev.enabled=true" \
    --set "server.image.repository=docker.io/hashicorp/vault" \
    --set "injector.image.repository=docker.io/hashicorp/vault-k8s"


  $ helm status vault
  $ helm get manifest vault


oc exec -it vault-0 -- /bin/sh

vault auth enable kubernetes

vault write auth/kubernetes/config \
    kubernetes_host="https://$KUBERNETES_PORT_443_TCP_ADDR:443"


oc new-project vault-test

oc create sa webapp

oc exec -it vault-0 -- /bin/sh

exit

create sa

oc create sa webapp

or 

apiVersion: v1
kind: ServiceAccount
metadata:
  name: webapp

oc apply --filename service-account-webapp.yml




vault kv put secret/webapp/conhttps://developer.hashicorp.com/vault/tutorials/kubernetes/kubernetes-sidecarig username="static-user" \
    password="static-password"

vault kv get secret/webapp/config

vault policy write webapp - <<EOF
path "secret/data/webapp/config" {
  capabilities = ["read"]https://developer.hashicorp.com/vault/tutorials/kubernetes/kubernetes-sidecar



vault write auth/kubernetes/role/webapp \
    bound_service_account_names=webapp \
    bound_service_account_namespaces=vault-test \
    policies=webapp \
    ttl=24h


vault write auth/kubernetes/role/issues \
    bound_service_account_names=issues \
    bound_service_account_namespaces=vault-test \
    policies=issues \
    ttl=24h

vault write auth/kubernetes/role/temenos \
    bound_service_account_names=temenos \
    bound_service_account_namespaces=t24 \
    policies=temenos \
    ttl=24h
