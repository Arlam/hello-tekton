### Starting conditions:


Install Tekton cli
```shell script
# Get the tar.xz
curl -LO https://github.com/tektoncd/cli/releases/download/v0.17.1/tkn_0.17.1_Linux_x86_64.tar.gz
# Extract tkn to your PATH (e.g. /usr/local/bin)
sudo tar xvzf tkn_0.17.1_Linux_x86_64.tar.gz -C /usr/local/bin/ tkn
```

```shell script
minikube delete --all                 # in case if you want to start from scratch with your minikube
minikube config set memory 16000
minikube config set cpus 8
minikube config set disk-size 62000
minikube addons enable dashboard
minikube addons enable registry
# minikube addons enable registry-aliases  # ???
minikube start
minikube config view
```

- disk-size: 62000
- memory: 16000
- vm-driver: kvm2
- cpus: 8


To check the version:
```shell script
kubectl version 
```
````shell script
Client Version: version.Info{Major:"1", Minor:"20", GitVersion:"v1.20.5", GitCommit:"6b1d87acf3c8253c123756b9e61dac642678305f", GitTreeState:"clean", BuildDate:"2021-03-18T01:10:43Z", GoVersion:"go1.15.8", Compiler:"gc", Platform:"linux/amd64"}
Server Version: version.Info{Major:"1", Minor:"17", GitVersion:"v1.17.3", GitCommit:"06ad960bfd03b39c8310aaf92d1e7c12ce618213", GitTreeState:"clean", BuildDate:"2020-02-11T18:07:13Z", GoVersion:"go1.13.6", Compiler:"gc", Platform:"linux/amd64"}
````

### Run tekton
````shell
kubectl apply --filename https://storage.googleapis.com/tekton-releases/pipeline/latest/release.yaml
```` 

### Run hello world
```shell script
kubectl create namespace tektontutorial
kubectl config set-context --current --namespace=tektontutorial
kubectl apply -f ./hello-task.yml --namespace=tektontutorial

#to show result
tkn task describe echo-hello-world -n tektontutorial
```

### Run PMD

### Build & use local image
* Point to minikube
    ```shell script
    eval $(minikube docker-env)
    ```
* Build image
    ```shell script
    docker build . -t localhost:5000/${IMG_NAME}:${TAG}
    ```
* Push image to minikube registry
    ```shell script
    docker push localhost:5000/${IMG_NAME}:${TAG}
    ```


### References 
* https://redhat-scholars.github.io/tekton-tutorial/tekton-tutorial/index.html
* https://tanzu.vmware.com/developer/guides/ci-cd/tekton-gs-p1/
