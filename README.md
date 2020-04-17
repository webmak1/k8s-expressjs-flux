# GitOps using Helm3 and Flux for a Node.js and Express.js Microservice

https://www.civo.com/learn/gitops-using-helm3-and-flux-for-an-node-js-and-express-js-microservice


<br/>

### Run in minikube


```
$ {
minikube --profile my-profile config set memory 4096
minikube --profile my-profile config set cpus 2

// $ minikube --profile my-profile config set vm-driver virtualbox
minikube --profile my-profile config set vm-driver docker

minikube --profile my-profile config set kubernetes-version v1.16.1
minikube start --profile my-profile
}
```

<br/>

    // To delete
    // $ minikube --profile my-profile stop && minikube --profile my-profile delete

<br/>

    $ kubectl version --short
    Client Version: v1.18.1
    Server Version: v1.16.1

<br/>

    // FluxCtl Installation
    $ curl -sL https://fluxcd.io/install | sh && chmod +x $HOME/.fluxcd/bin/fluxctl && sudo mv $HOME/.fluxcd/bin/fluxctl /usr/local/bin/


<br/>

### With HELM3

    $ helm repo add fluxcd https://charts.fluxcd.io
    
    $ kubectl create namespace fluxcd
    
    $ helm upgrade -i flux fluxcd/flux --wait \
    --namespace fluxcd \
    --set git.url=git@github.com:webmakaka/k8s-expressjs-flux \
    --set git.timeout=3m \
    --set git.pollInterval=1m \
    --set resources.requests.cpu=500m \
    --set resources.requests.memory=500Mi \
    --set sync.timeout=3m \
    --set helm.versions=v3


    $ kubectl apply -f https://raw.githubusercontent.com/fluxcd/helm-operator/master/deploy/crds.yaml


    $ helm upgrade -i helm-operator fluxcd/helm-operator --wait \
    --namespace fluxcd \
    --set git.ssh.secretName=flux-git-deploy \
    --set helm.versions=v3
    
    $ watch kubectl -n fluxcd get pods
    
    $ fluxctl --k8s-fwd-ns fluxcd identity 
     
     GITHUB --> Project (flux-get-started) --> SETTINGS --> DELPLOY KEYS

    + allow write access
    
<br/>

    $ fluxctl --k8s-fwd-ns=fluxcd sync

    $ kubectl -n fluxcd logs deployment/flux -f


<br/>

// Still here  <br/>
https://alexellis.github.io/expressjs-k8s/index.yaml

<br/>

```
$ kubectl get helmrelease  -A
NAMESPACE   NAME            RELEASE                 PHASE       STATUS     MESSAGE                                                                         AGE
default     expressjs-k8s   default-expressjs-k8s   Succeeded   deployed   Release was successful for Helm release 'default-expressjs-k8s' in 'default'.   3m2s
```

    $ kubectl describe helmrelease/expressjs-k8s

    $ kubectl get deploy -o wide


<br/>

    $ kubectl port-forward deploy/default-expressjs-k8s 8080:8080 &

<!--

    $ minikube --profile my-profile  ip
    172.17.0.2

-->

    $ sudo apt install -y jq


 ```
 $ curl -s localhost:8080/links |jq
[
  {
    "name": "github",
    "url": "https://github.com/alexellis"
  },
  {
    "name": "twitter",
    "url": "https://twitter.com/alexellisuk"
  },
  {
    "name": "blog",
    "url": "https://blog.alexellis.io"
  },
  {
    "name": "sponsors",
    "url": "https://github.com/users/alexellis/sponsorship"
  }
]

```


http://localhost:8080/


<br/>

Works...   
I do not understand why...    
May be because i use docker driver for minikube...

<br/>

```
$ kubectl  describe pod default-expressjs-k8s-64bf68f8d9-sv8cw | grep Image
    Image:          alexellis2/service:0.3.7
    Image ID:       docker-pullable://alexellis2/service@sha256:5437f3f8cd862f643732c432a678794b3f96ce27fe4635a77aba9e1b653485f5
```

<br/>

    $ kubectl get helmrelease/expressjs-k8s -o yaml


---

<strong>Marley</strong>

<a href="https://webmakaka.com"><strong>WebMakaka</strong></a>