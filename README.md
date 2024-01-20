# kubeflow-demo
Learning how to work with Kubeflow locally to do MLOps.

### Using local microk8s
- `brew install multipass`
- `brew install ubuntu/microk8s/microk8s`
- `microk8s install --channel=1.22/stable`
- `microk8s status --wait-ready`
- `microk8s enable dns ingress registry storage istio`
- `microk8s kubectl get all --all-namespaces`
- `brew install juju`
- `juju bootstrap microk8s my-controller`
- `juju add-model kubeflow`
- `juju deploy kubeflow-lite --trust`
- `brew install watch`
- `watch -c juju status --color` (run this in a separate terminal window)
- `watch -c microk8s kubectl get po -n kubeflow` (run this in a separate terminal window)

### Charmed Kubeflow
- `brew install multipass`
- `multipass launch --cpus 8 --memory 12G --disk 40G --name tutorial-vm charm-dev`
- `multipass shell tutorial-vm`
- `snap list`
- `sudo snap refresh microk8s --channel=1.22/stable --classic` (this is due to kubeflow not working with newer versions of microk8s)
- `microk8s status --wait-ready`
- `kubectl get all --all-namespaces`
- `kubectl get po -A`
- `juju models`
- `juju controllers`
- `juju add-k8s myk8s`
- `juju clouds`
- `juju bootstrap myk8s my-controller`
- `kubectl get namespaces`
- `juju add-model kubeflow`
- `juju deploy kubeflow-lite --trust`
- `watch -c juju status --color`
- `watch -c kubectl get po -n kubeflow`

- `kubectl patch role -n kubeflow istio-ingressgateway-operator -p '{"apiVersion":"rbac.authorization.k8s.io/v1","kind":"Role","metadata":{"name":"istio-ingressgateway-operator"},"rules":[{"apiGroups":["*"],"resources":["*"],"verbs":["*"]}]}'`

- https://charmed-kubeflow.io/docs/get-started-with-charmed-kubeflow (following the steps here in the multipass ubuntu shell)
- `sudo snap install microk8s --classic --channel=1.26/stable`
- `sudo snap install juju --classic --channel=2.9/stable`
- `sudo addgroup --system microk8s`
- `sudo adduser $USER microk8s`
- `sudo usermod -a -G microk8s $USER`
- `newgrp microk8s` Note: You’ll need to re-run newgrp microk8s any time you open a new shell session.
- `sudo chown -f -R $USER ~/.kube`
- `sudo microk8s enable dns hostpath-storage ingress metallb:10.64.140.43-10.64.140.49 dashboard`
- `microk8s status`
- `microk8s kubectl get all --all-namespaces`
- `microk8s config | juju add-k8s my-k8s --client`
- `juju bootstrap my-k8s uk8sx`
- `juju add-model kubeflow`
- `sudo sysctl fs.inotify.max_user_instances=1280`
- `sudo sysctl fs.inotify.max_user_watches=655360`
- `juju deploy kubeflow --trust  --channel=1.8/stable`
- `watch -c juju status --color`

- `juju bootstrap microk8s micro`  (don't think this is needed)
- `juju add-model kubeflow`
- `juju deploy kubeflow --trust`
- `juju status` or `watch -c juju status --color`
- `kubectl get services -n kubeflow` (find the istio-ingressgateway IP address here)
- `juju config dex-auth public-url=http://<IP address>` (from above)
- `juju config oidc-gatekeeper public-url=http://<IP address>` (from above) - these are necessary to make the kubeflow dashboard accessible
- `juju config dex-auth static-username=admin`
- `juju config dex-auth static-password=admin`
- access the kubeflow dashboard at http://<IP address>.nip.io/ (using the IP address from above and credentials from above)


- `multipass delete --all --purge`

