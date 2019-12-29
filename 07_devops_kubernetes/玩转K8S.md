
# 玩转K8S

## 00 先跑起来

We are the Borg.
lower your shields and surrender your ships.
we will add your biological and technological distinctiveness to our own.
Your culture will adapt to service us.
Resistance is futile.

![玩转K8S-What is Brog](img/000_borg.png)

我们是博格。

放下你的盾牌，投降你的船。

我们将把你的生物和技术的独特性加入我们自己的领域。

你们的文化将适应我们的服务。
**
反抗是徒劳的。


### 方法1：在线交互环境 

	https://kubernetes.io/docs/tutorials/kubernetes-basics/create-cluster/cluster-interactive/


### 方法2：Windows版本的Minkube

	https://kubernetes.io/docs/tutorials/hello-minikube/
	minikube start --registry-mirror=https://registry.docker-cn.com --kubernetes-version v1.12.1
	minikube version: v0.30.0

### 方法3：Linux版本的K8S机器

	[root@master mac]# kubeadm version
	kubeadm version: &version.Info{
	Major:"1", Minor:"15", 
	GitVersion:"v1.15.0", 
	GitCommit:"e8462b5b5dc2584fdcd18e6bcfe9f1e4d970a529", 
	GitTreeState:"clean", 
	BuildDate:"2019-06-19T16:37:41Z", 
	GoVersion:"go1.12.5", 
	Compiler:"gc", Platform:"linux/amd64"}

	[root@master mac]# kubectl version
	Client Version: version.Info{
	Major:"1", Minor:"15", GitVersion:"v1.15.0", 
	GitCommit:"e8462b5b5dc2584fdcd18e6bcfe9f1e4d970a529", GitTreeState:"clean", BuildDate:"2019-06-19T16:40:16Z", GoVersion:"go1.12.5", Compiler:"gc", Platform:"linux/amd64"}
	Server Version: version.Info{Major:"1", Minor:"15", GitVersion:"v1.15.0", GitCommit:"e8462b5b5dc2584fdcd18e6bcfe9f1e4d970a529", GitTreeState:"clean", BuildDate:"2019-06-19T16:32:14Z", GoVersion:"go1.12.5", Compiler:"gc", Platform:"linux/amd64"}

	[root@master mac]# kubelet --version
	Kubernetes v1.15.0

### 帮助 kubectl run -h

	[root@master mac]# kubectl run -h
	Create and run a particular image, possibly replicated.
	
	 Creates a deployment or job to manage the created container(s).
	
	Examples:
	  # Start a single instance of nginx.
	  kubectl run nginx --image=nginx
	  
	  # Start a single instance of hazelcast and let the container expose port 5701 .
	  kubectl run hazelcast --image=hazelcast --port=5701
	  
	  # Start a single instance of hazelcast and set environment variables "DNS_DOMAIN=cluster" and "POD_NAMESPACE=default"
	in the container.
	  kubectl run hazelcast --image=hazelcast --env="DNS_DOMAIN=cluster" --env="POD_NAMESPACE=default"
	  
	  # Start a single instance of hazelcast and set labels "app=hazelcast" and "env=prod" in the container.
	  kubectl run hazelcast --image=hazelcast --labels="app=hazelcast,env=prod"
	  
	  # Start a replicated instance of nginx.
	  kubectl run nginx --image=nginx --replicas=5
	  
	  # Dry run. Print the corresponding API objects without creating them.
	  kubectl run nginx --image=nginx --dry-run
	  
	  # Start a single instance of nginx, but overload the spec of the deployment with a partial set of values parsed from
	JSON.
	  kubectl run nginx --image=nginx --overrides='{ "apiVersion": "v1", "spec": { ... } }'
	  
	  # Start a pod of busybox and keep it in the foreground, don't restart it if it exits.
	  kubectl run -i -t busybox --image=busybox --restart=Never
	  
	  # Start the nginx container using the default command, but use custom arguments (arg1 .. argN) for that command.
	  kubectl run nginx --image=nginx -- <arg1> <arg2> ... <argN>
	  
	  # Start the nginx container using a different command and custom arguments.
	  kubectl run nginx --image=nginx --command -- <cmd> <arg1> ... <argN>
	  
	  # Start the perl container to compute π to 2000 places and print it out.
	  kubectl run pi --image=perl --restart=OnFailure -- perl -Mbignum=bpi -wle 'print bpi(2000)'
	  
	  # Start the cron job to compute π to 2000 places and print it out every 5 minutes.
	  kubectl run pi --schedule="0/5 * * * ?" --image=perl --restart=OnFailure -- perl -Mbignum=bpi -wle 'print bpi(2000)'
	
	Options:
	      --allow-missing-template-keys=true: If true, ignore any errors in templates when a field or map key is missing in
	the template. Only applies to golang and jsonpath output formats.
	      --attach=false: If true, wait for the Pod to start running, and then attach to the Pod as if 'kubectl attach ...'
	were called.  Default false, unless '-i/--stdin' is set, in which case the default is true. With '--restart=Never' the
	exit code of the container process is returned.
	      --cascade=true: If true, cascade the deletion of the resources managed by this resource (e.g. Pods created by a
	ReplicationController).  Default true.
	      --command=false: If true and extra arguments are present, use them as the 'command' field in the container, rather
	than the 'args' field which is the default.
	      --dry-run=false: If true, only print the object that would be sent, without sending it.
	      --env=[]: Environment variables to set in the container
	      --expose=false: If true, a public, external service is created for the container(s) which are run
	  -f, --filename=[]: to use to replace the resource.
	      --force=false: Only used when grace-period=0. If true, immediately remove resources from API and bypass graceful
	deletion. Note that immediate deletion of some resources may result in inconsistency or data loss and requires
	confirmation.
	      --generator='': The name of the API generator to use, see
	http://kubernetes.io/docs/user-guide/kubectl-conventions/#generators for a list.
	      --grace-period=-1: Period of time in seconds given to the resource to terminate gracefully. Ignored if negative.
	Set to 1 for immediate shutdown. Can only be set to 0 when --force is true (force deletion).
	      --hostport=-1: The host port mapping for the container port. To demonstrate a single-machine container.
	      --image='': The image for the container to run.
	      --image-pull-policy='': The image pull policy for the container. If left empty, this value will not be specified
	by the client and defaulted by the server
	  -k, --kustomize='': Process a kustomization directory. This flag can't be used together with -f or -R.
	  -l, --labels='': Comma separated labels to apply to the pod(s). Will override previous values.
	      --leave-stdin-open=false: If the pod is started in interactive mode or with stdin, leave stdin open after the
	first attach completes. By default, stdin will be closed after the first attach completes.
	      --limits='': The resource requirement limits for this container.  For example, 'cpu=200m,memory=512Mi'.  Note that
	server side components may assign limits depending on the server configuration, such as limit ranges.
	  -o, --output='': Output format. One of:
	json|yaml|name|go-template|go-template-file|template|templatefile|jsonpath|jsonpath-file.
	      --overrides='': An inline JSON override for the generated object. If this is non-empty, it is used to override the
	generated object. Requires that the object supply a valid apiVersion field.
	      --pod-running-timeout=1m0s: The length of time (like 5s, 2m, or 3h, higher than zero) to wait until at least one
	pod is running
	      --port='': The port that this container exposes.  If --expose is true, this is also the port used by the service
	that is created.
	      --quiet=false: If true, suppress prompt messages.
	      --record=false: Record current kubectl command in the resource annotation. If set to false, do not record the
	command. If set to true, record the command. If not set, default to updating the existing annotation value only if one
	already exists.
	  -R, --recursive=false: Process the directory used in -f, --filename recursively. Useful when you want to manage
	related manifests organized within the same directory.
	  -r, --replicas=1: Number of replicas to create for this container. Default is 1.
	      --requests='': The resource requirement requests for this container.  For example, 'cpu=100m,memory=256Mi'.  Note
	that server side components may assign requests depending on the server configuration, such as limit ranges.
	      --restart='Always': The restart policy for this Pod.  Legal values [Always, OnFailure, Never].  If set to 'Always'
	a deployment is created, if set to 'OnFailure' a job is created, if set to 'Never', a regular pod is created. For the
	latter two --replicas must be 1.  Default 'Always', for CronJobs `Never`.
	      --rm=false: If true, delete resources created in this command for attached containers.
	      --save-config=false: If true, the configuration of current object will be saved in its annotation. Otherwise, the
	annotation will be unchanged. This flag is useful when you want to perform kubectl apply on this object in the future.
	      --schedule='': A schedule in the Cron format the job should be run with.
	      --service-generator='service/v2': The name of the generator to use for creating a service.  Only used if --expose
	is true
	      --service-overrides='': An inline JSON override for the generated service object. If this is non-empty, it is used
	to override the generated object. Requires that the object supply a valid apiVersion field.  Only used if --expose is
	true.
	      --serviceaccount='': Service account to set in the pod spec
	  -i, --stdin=false: Keep stdin open on the container(s) in the pod, even if nothing is attached.
	      --template='': Template string or path to template file to use when -o=go-template, -o=go-template-file. The
	template format is golang templates [http://golang.org/pkg/text/template/#pkg-overview].
	      --timeout=0s: The length of time to wait before giving up on a delete, zero means determine a timeout from the
	size of the object
	  -t, --tty=false: Allocated a TTY for each container in the pod.
	      --wait=false: If true, wait for resources to be gone before returning. This waits for finalizers.
	
	Usage:
	  kubectl run NAME --image=image [--env="key=value"] [--port=port] [--replicas=replicas] [--dry-run=bool]
	[--overrides=inline-json] [--command] -- [COMMAND] [args...] [options]
	
	Use "kubectl options" for a list of global command-line options (applies to all commands).
	[root@master mac]# 

## 01 环境检查

### 查看集群信息

	[root@master mac]# kubectl cluster-info
	Kubernetes master is running at https://192.168.0.106:6443
	KubeDNS is running at https://192.168.0.106:6443/api/v1/namespaces/kube-system/services/kube-dns:dns/proxy
	To further debug and diagnose cluster problems, use 'kubectl cluster-info dump'.
	[root@master mac]# 

### 查看节点信息

	[root@master mac]# kubectl get nodes
	NAME         STATUS   ROLES    AGE   VERSION
	master.k8s   Ready    master   4d    v1.15.0
	node1.k8s    Ready    <none>   4d    v1.15.0
	node2.k8s    Ready    <none>   4d    v1.15.0
	[root@master mac]# 

### 查看机器信息

	[root@master mac]# hostname
	master.k8s
	[root@master mac]# 
	
	[root@master mac]# ping node1.k8s
	PING node1.k8s (192.168.0.107) 56(84) bytes of data.
	64 bytes from node1.k8s (192.168.0.107): icmp_seq=1 ttl=64 time=0.599 ms
	64 bytes from node1.k8s (192.168.0.107): icmp_seq=2 ttl=64 time=0.336 ms
	64 bytes from node1.k8s (192.168.0.107): icmp_seq=3 ttl=64 time=0.415 ms
	--- node1.k8s ping statistics ---
	3 packets transmitted, 3 received, 0% packet loss, time 2001ms
	rtt min/avg/max/mdev = 0.336/0.450/0.599/0.110 ms
	[root@master mac]# 
	
	[root@master mac]# ping node2.k8s
	PING node2.k8s (192.168.0.108) 56(84) bytes of data.
	64 bytes from node2.k8s (192.168.0.108): icmp_seq=1 ttl=64 time=0.282 ms
	64 bytes from node2.k8s (192.168.0.108): icmp_seq=2 ttl=64 time=0.359 ms
	64 bytes from node2.k8s (192.168.0.108): icmp_seq=3 ttl=64 time=0.353 ms
	--- node2.k8s ping statistics ---
	6 packets transmitted, 6 received, 0% packet loss, time 4999ms
	rtt min/avg/max/mdev = 0.260/0.314/0.359/0.043 ms
	[root@master mac]# 

### 查看可以的资源

	[root@master mac]# kubectl get pods
	No resources found.
	[root@master mac]# 
	
	[root@master mac]# kubectl get services
	NAME         TYPE        CLUSTER-IP   EXTERNAL-IP   PORT(S)   AGE
	kubernetes   ClusterIP   10.96.0.1    <none>        443/TCP   4d
	[root@master mac]# 

## 02 部署应用

### 使用 jocatalin/kubernetes-bootcamp

	https://hub.docker.com/r/jocatalin/kubernetes-bootcamp

### 提前获取镜像

注意： 我们使用**V1**和**V2**镜像，为了演示滚动升级的效果。

	[root@master mac]# docker pull jocatalin/kubernetes-bootcamp:v1
	Trying to pull repository docker.io/jocatalin/kubernetes-bootcamp ... 
	v1: Pulling from docker.io/jocatalin/kubernetes-bootcamp
	5c90d4a2d1a8: Pull complete 
	ab30c63719b1: Pull complete 
	29d0bc1e8c52: Pull complete 
	d4fe0dc68927: Pull complete 
	dfa9e924f957: Pull complete 
	Digest: sha256:0d6b8ee63bb57c5f5b6156f446b3bc3b3c143d233037f3a2f00e279c8fcc64af
	Status: Downloaded newer image for docker.io/jocatalin/kubernetes-bootcamp:v1
	[root@master mac]# 
	
	[root@master mac]# docker pull jocatalin/kubernetes-bootcamp:v2
	Trying to pull repository docker.io/jocatalin/kubernetes-bootcamp ... 
	v2: Pulling from docker.io/jocatalin/kubernetes-bootcamp
	5c90d4a2d1a8: Already exists 
	ab30c63719b1: Already exists 
	29d0bc1e8c52: Already exists 
	d4fe0dc68927: Already exists 
	8cbcd299f923: Pull complete 
	Digest: sha256:fb1a3ced00cecfc1f83f18ab5cd14199e30adc1b49aa4244f5d65ad3f5feb2a5
	Status: Downloaded newer image for docker.io/jocatalin/kubernetes-bootcamp:v2
	[root@master mac]# 

### kubectl run kubernetes-bootcamp --generator=deployment/apps.v1 (DEPRECATED)

	[root@master mac]# kubectl run kubernetes-bootcamp --image=docker.io/jocatalin/kubernetes-bootcamp:v1 --port=8080
	kubectl run --generator=deployment/apps.v1 is DEPRECATED and will be removed in a future version. 
	Use kubectl run --generator=run-pod/v1 or kubectl create instead.
	deployment.apps/kubernetes-bootcamp created
	[root@master mac]# 

### 查看Pod

	[root@master mac]# kubectl get pods
	NAME                                   READY   STATUS    RESTARTS   AGE
	kubernetes-bootcamp-7dc9765bf6-hx9rd   1/1     Running   0          79s
	[root@master mac]# 

	[root@master mac]# kubectl get pods -o wide
	NAME                                   READY   STATUS    RESTARTS   AGE   IP          NODE        NOMINATED NODE   READINESS GATES
	kubernetes-bootcamp-7dc9765bf6-hx9rd   1/1     Running   0          82s   10.38.0.1   node1.k8s   <none>           <none>
	[root@master mac]# 

## 03 访问应用

### 查看服务

	[root@master mac]# kubectl get services
	NAME         TYPE        CLUSTER-IP   EXTERNAL-IP   PORT(S)   AGE
	kubernetes   ClusterIP   10.96.0.1    <none>        443/TCP   4d1h
	[root@master mac]# 

### 暴露服务

	[root@master mac]# kubectl expose deployment/kubernetes-bootcamp --type="NodePort" --port 8080
	service/kubernetes-bootcamp exposed
	[root@master mac]# 

### 重现查看服务

	[root@master mac]# kubectl get services
	NAME                  TYPE        CLUSTER-IP       EXTERNAL-IP   PORT(S)          AGE
	kubernetes            ClusterIP   10.96.0.1        <none>        443/TCP          4d1h
	kubernetes-bootcamp   NodePort    10.108.203.219   <none>        8080:31828/TCP   6s

### 测试应用

	[root@master mac]# curl node1.k8s:31828
	Hello Kubernetes bootcamp! | Running on: kubernetes-bootcamp-7dc9765bf6-hx9rd | v=1
	[root@master mac]# 


## 04 伸缩应用

### 当前是单一副本

	[root@master mac]# kubectl get deployments
	NAME                  READY   UP-TO-DATE   AVAILABLE   AGE
	kubernetes-bootcamp   1/1     1            1           8m15s
	[root@master mac]# 

### 增加副本到3个

	[root@master mac]# kubectl scale deployment/kubernetes-bootcamp --replicas=3
	deployment.extensions/kubernetes-bootcamp scaled
	[root@master mac]# 

### 查看ScaleUp情况

	[root@master mac]# kubectl get pods
	NAME                                   READY   STATUS              RESTARTS   AGE
	kubernetes-bootcamp-7dc9765bf6-hx9rd   1/1     Running             0          8m48s
	kubernetes-bootcamp-7dc9765bf6-schrp   0/1     ContainerCreating   0          8s
	kubernetes-bootcamp-7dc9765bf6-v2hbf   1/1     Running             0          8s
	[root@master mac]# 

	[root@master mac]# kubectl get pods -o wide
	NAME                                   READY   STATUS    RESTARTS   AGE   IP          NODE        NOMINATED NODE   READINESS GATES
	kubernetes-bootcamp-7dc9765bf6-hx9rd   1/1     Running   0          10m   10.38.0.1   node1.k8s   <none>           <none>
	kubernetes-bootcamp-7dc9765bf6-schrp   1/1     Running   0          88s   10.32.0.2   node2.k8s   <none>           <none>
	kubernetes-bootcamp-7dc9765bf6-v2hbf   1/1     Running   0          88s   10.38.0.2   node1.k8s   <none>           <none>
	[root@master mac]# 

### 减少副本到2个

	[root@master mac]# kubectl scale deployment/kubernetes-bootcamp --replicas=2
	deployment.extensions/kubernetes-bootcamp scaled
	[root@master mac]# 

### 查看ScaleDown情况

	[root@master mac]# kubectl get pods -o wide
	NAME                                   READY   STATUS        RESTARTS   AGE   IP          NODE        NOMINATED NODE   READINESS GATES
	kubernetes-bootcamp-7dc9765bf6-hx9rd   1/1     Running       0          27m   10.38.0.1   node1.k8s   <none>           <none>
	kubernetes-bootcamp-7dc9765bf6-schrp   1/1     Terminating   0          19m   10.32.0.2   node2.k8s   <none>           <none>
	kubernetes-bootcamp-7dc9765bf6-v2hbf   1/1     Running       0          19m   10.38.0.2   node1.k8s   <none>           <none>
	[root@master mac]# 
	[root@master mac]# kubectl get pods -o wide
	NAME                                   READY   STATUS    RESTARTS   AGE   IP          NODE        NOMINATED NODE   READINESS GATES
	kubernetes-bootcamp-7dc9765bf6-hx9rd   1/1     Running   0          29m   10.38.0.1   node1.k8s   <none>           <none>
	kubernetes-bootcamp-7dc9765bf6-v2hbf   1/1     Running   0          20m   10.38.0.2   node1.k8s   <none>           <none>
	[root@master mac]# 

### 测试负载均衡

	[root@master mac]# kubectl get services
	NAME                  TYPE        CLUSTER-IP       EXTERNAL-IP   PORT(S)          AGE
	kubernetes            ClusterIP   10.96.0.1        <none>        443/TCP          4d1h
	kubernetes-bootcamp   NodePort    10.108.203.219   <none>        8080:31828/TCP   31m
	[root@master mac]# 

	[root@master mac]# curl master.k8s:31828
	Hello Kubernetes bootcamp! | Running on: kubernetes-bootcamp-7dc9765bf6-hx9rd | v=1
	[root@master mac]# curl master.k8s:31828
	Hello Kubernetes bootcamp! | Running on: kubernetes-bootcamp-7dc9765bf6-v2hbf | v=1
	[root@master mac]# curl master.k8s:31828
	Hello Kubernetes bootcamp! | Running on: kubernetes-bootcamp-7dc9765bf6-hx9rd | v=1
	[root@master mac]# curl master.k8s:31828
	Hello Kubernetes bootcamp! | Running on: kubernetes-bootcamp-7dc9765bf6-v2hbf | v=1
	[root@master mac]# 

	[root@master mac]# curl 10.108.203.219:8080
	Hello Kubernetes bootcamp! | Running on: kubernetes-bootcamp-7dc9765bf6-hx9rd | v=1
	[root@master mac]# curl 10.108.203.219:8080
	Hello Kubernetes bootcamp! | Running on: kubernetes-bootcamp-7dc9765bf6-v2hbf | v=1
	[root@master mac]# curl 10.108.203.219:8080
	Hello Kubernetes bootcamp! | Running on: kubernetes-bootcamp-7dc9765bf6-hx9rd | v=1
	[root@master mac]# curl 10.108.203.219:8080
	Hello Kubernetes bootcamp! | Running on: kubernetes-bootcamp-7dc9765bf6-v2hbf | v=1
	[root@master mac]# 

	[root@master mac]# kubectl get pods
	NAME                                   READY   STATUS    RESTARTS   AGE
	kubernetes-bootcamp-7dc9765bf6-hx9rd   1/1     Running   0          32m
	kubernetes-bootcamp-7dc9765bf6-v2hbf   1/1     Running   0          23m
	[root@master mac]# 

	[root@master mac]# kubectl get pods -o wide
	NAME                                   READY   STATUS    RESTARTS   AGE   IP          NODE        NOMINATED NODE   READINESS GATES
	kubernetes-bootcamp-7dc9765bf6-hx9rd   1/1     Running   0          35m   10.38.0.1   node1.k8s   <none>           <none>
	kubernetes-bootcamp-7dc9765bf6-v2hbf   1/1     Running   0          26m   10.38.0.2   node1.k8s   <none>           <none>
	[root@master mac]# 

## 05 滚动更新

### 升级为V2版本

	[root@master mac]# kubectl set image deployment/kubernetes-bootcamp kubernetes-bootcamp=jocatalin/kubernetes-bootcamp:v2
	deployment.extensions/kubernetes-bootcamp image updated
	[root@master mac]# 

### 查看升级情况

	[root@master mac]# kubectl get pods
	NAME                                   READY   STATUS              RESTARTS   AGE
	kubernetes-bootcamp-7dc9765bf6-hx9rd   1/1     Running             0          36m
	kubernetes-bootcamp-7dc9765bf6-v2hbf   1/1     Running             0          28m
	kubernetes-bootcamp-cfc74666-mfh6x     0/1     ContainerCreating   0          14s
	[root@master mac]# 

	[root@master mac]# kubectl get pods -o wide
	NAME                                   READY   STATUS              RESTARTS   AGE   IP          NODE        NOMINATED NODE   READINESS GATES
	kubernetes-bootcamp-7dc9765bf6-hx9rd   1/1     Running             0          37m   10.38.0.1   node1.k8s   <none>           <none>
	kubernetes-bootcamp-7dc9765bf6-v2hbf   1/1     Terminating         0          28m   10.38.0.2   node1.k8s   <none>           <none>
	kubernetes-bootcamp-cfc74666-lswgs     0/1     ContainerCreating   0          7s    <none>      node1.k8s   <none>           <none>
	kubernetes-bootcamp-cfc74666-mfh6x     1/1     Running             0          22s   10.32.0.2   node2.k8s   <none>           <none>
	[root@master mac]# 

	[root@master mac]# kubectl get pods
	NAME                                   READY   STATUS        RESTARTS   AGE
	kubernetes-bootcamp-7dc9765bf6-hx9rd   1/1     Terminating   0          37m
	kubernetes-bootcamp-7dc9765bf6-v2hbf   1/1     Terminating   0          28m
	kubernetes-bootcamp-cfc74666-lswgs     1/1     Running       0          26s
	kubernetes-bootcamp-cfc74666-mfh6x     1/1     Running       0          41s
	[root@master mac]# 

### 测试应用的升级

	[root@master mac]# curl master.k8s:8080
	curl: (7) Failed connect to master.k8s:8080; Connection refused
	[root@master mac]# 

	[root@master mac]# curl master.k8s:31828
	Hello Kubernetes bootcamp! | Running on: kubernetes-bootcamp-cfc74666-lswgs | v=2
	[root@master mac]# curl master.k8s:31828
	Hello Kubernetes bootcamp! | Running on: kubernetes-bootcamp-cfc74666-lswgs | v=2
	[root@master mac]# curl master.k8s:31828
	Hello Kubernetes bootcamp! | Running on: kubernetes-bootcamp-cfc74666-mfh6x | v=2
	[root@master mac]# curl master.k8s:31828
	Hello Kubernetes bootcamp! | Running on: kubernetes-bootcamp-cfc74666-lswgs | v=2
	[root@master mac]# curl master.k8s:31828
	Hello Kubernetes bootcamp! | Running on: kubernetes-bootcamp-cfc74666-mfh6x | v=2
	[root@master mac]# 

### 查看Pods的详细情况

	[root@master mac]# kubectl get pods -o wide
	NAME                                 READY   STATUS    RESTARTS   AGE    IP          NODE        NOMINATED NODE   READINESS GATES
	kubernetes-bootcamp-cfc74666-lswgs   1/1     Running   0          92s    10.38.0.3   node1.k8s   <none>           <none>
	kubernetes-bootcamp-cfc74666-mfh6x   1/1     Running   0          107s   10.32.0.2   node2.k8s   <none>           <none>

### 回滚应用

	[root@master mac]# kubectl rollout undo deployment/kubernetes-bootcamp
	deployment.extensions/kubernetes-bootcamp rolled back
	[root@master mac]# 

### 查看Pods的详细情况

	[root@master mac]# kubectl get pods
	NAME                                   READY   STATUS        RESTARTS   AGE
	kubernetes-bootcamp-7dc9765bf6-hvh6k   1/1     Running       0          6s
	kubernetes-bootcamp-7dc9765bf6-pnh6s   1/1     Running       0          8s
	kubernetes-bootcamp-cfc74666-lswgs     1/1     Terminating   0          5m56s
	kubernetes-bootcamp-cfc74666-mfh6x     1/1     Terminating   0          6m11s
	[root@master mac]# 

### 验证版本回退到V1

	[root@master mac]# curl master.k8s:31828
	Hello Kubernetes bootcamp! | Running on: kubernetes-bootcamp-7dc9765bf6-pnh6s | v=1
	[root@master mac]# curl master.k8s:31828
	Hello Kubernetes bootcamp! | Running on: kubernetes-bootcamp-7dc9765bf6-hvh6k | v=1
	[root@master mac]# 


## 06 重要概念

### Cluster

### Master

API Server （kube-apiserver）,提供了HTTP/HTTPs RESTFul API。

	[root@master demo_k8s]# kubectl api-versions
	admissionregistration.k8s.io/v1beta1
	apiextensions.k8s.io/v1beta1
	apiregistration.k8s.io/v1
	apiregistration.k8s.io/v1beta1
	apps/v1
	apps/v1beta1
	apps/v1beta2
	authentication.k8s.io/v1
	authentication.k8s.io/v1beta1
	authorization.k8s.io/v1
	authorization.k8s.io/v1beta1
	autoscaling/v1
	autoscaling/v2beta1
	autoscaling/v2beta2
	batch/v1
	batch/v1beta1
	certificates.k8s.io/v1beta1
	coordination.k8s.io/v1
	coordination.k8s.io/v1beta1
	events.k8s.io/v1beta1
	extensions/v1beta1
	networking.k8s.io/v1
	networking.k8s.io/v1beta1
	node.k8s.io/v1beta1
	policy/v1beta1
	rbac.authorization.k8s.io/v1
	rbac.authorization.k8s.io/v1beta1
	scheduling.k8s.io/v1
	scheduling.k8s.io/v1beta1
	storage.k8s.io/v1
	storage.k8s.io/v1beta1
	v1
	[root@master demo_k8s]# 


### Node

### Pod

### Controller

### Service

### Namespace

## 07 搭建K8S集群

### 操作系统和软件包

	VMware Workstation Pro 12 
	CentOS 7 minimal ISO

### 创建虚拟机

	硬盘20G
	内存2G
	网络是桥接模式

### 安装操作系统

	最小化安装，保持语言为英文
	配置好ROOT帐号
	配置好主机名： master.k8s

### 第一次登录
	
	激活网卡
	禁用SELinux
	禁用防火墙

### 禁用SELinux
	
	# 临时
	# setenforce 0
	
	# 永久
	[root@master mac]# vi /etc/selinux/config 
	change: SELINUX=enforcing  
	as:
	SELINUX=permissive

### 禁用防火墙

	[root@master mac]# systemctl disable firewalld && systemctl stop firewalld
	Removed symlink /etc/systemd/system/multi-user.target.wants/firewalld.service.
	Removed symlink /etc/systemd/system/dbus-org.fedoraproject.FirewallD1.service.
	[root@master mac]# 

### 在YUM仓库中添加K8s

由于墙的原因无法直接访问到Google的软件仓库(packages.cloud.google.com)和容器仓库(gcr.io)，解决方法有两种：

	一是直接配置的Hosts文件
	二是使用三方源或转存的容器仓库

### 三方源或转存的容器仓库

	cat <<EOF > /etc/yum.repos.d/kubernetes.repo
	[kubernetes]
	name=Kubernetes
	baseurl=http://mirrors.aliyun.com/kubernetes/yum/repos/kubernetes-el7-x86_64
	enabled=1
	gpgcheck=0
	repo_gpgcheck=0
	gpgkey=http://mirrors.aliyun.com/kubernetes/yum/doc/yum-key.gpg
	        http://mirrors.aliyun.com/kubernetes/yum/doc/rpm-package-key.gpg
	EOF

### 直接配置的Hosts文件

	[root@master mac]# vi /etc/hosts
	127.0.0.1   localhost localhost.localdomain localhost4 localhost4.localdomain4
	::1         localhost localhost.localdomain localhost6 localhost6.localdomain6
	
	74.125.206.210 gcr.io
	74.125.206.210 www.gcr.io
	74.125.206.210 packages.cloud.google.com

	cat <<EOF > /etc/yum.repos.d/kubernetes.repo
	[kubernetes]
	name=Kubernetes
	baseurl=http://yum.kubernetes.io/repos/kubernetes-el7-x86_64
	enabled=1
	gpgcheck=1
	repo_gpgcheck=1
	gpgkey=http://packages.cloud.google.com/yum/doc/yum-key.gpg
	        http://packages.cloud.google.com/yum/doc/rpm-package-key.gpg
	EOF

### 安装Docker, Kubelet, Kubeadm, Kubectl, kubernetes-cni

	yum install -y docker 
    yum install -y kubelet kubeadm kubectl 
    yum install -y kubernetes-cni 

### 安装后配置Docker服务和Kubelet服务

    systemctl enable docker && systemctl start docker
    systemctl enable kubelet && systemctl start kubelet

### 启动net.bridge.bridge-nf-call-iptables内核选项

	[root@master mac]# sysctl -w net.bridge.bridge-nf-call-iptables=1
	net.bridge.bridge-nf-call-iptables = 1
	[root@master mac]# 
	[root@master mac]# echo "net.bridge.bridge-nf-call-iptables=1" > /etc/sysctl.d/k8s.conf
	[root@master mac]# cat /etc/sysctl.d/k8s.conf
	net.bridge.bridge-nf-call-iptables=1
	[root@master mac]# 


### 禁用交换分区

	[root@master mac]# swapoff -a && sed -i '/ swap / s/^/#/' /etc/fstab
	[root@master mac]# cat /etc/fstab 
	#
	# /etc/fstab
	# Created by anaconda on Sat Jun 29 14:31:05 2019
	#
	# Accessible filesystems, by reference, are maintained under '/dev/disk'
	# See man pages fstab(5), findfs(8), mount(8) and/or blkid(8) for more info
	#
	/dev/mapper/centos-root /                       xfs     defaults        0 0
	UUID=e90e3546-df4e-4b13-a67a-b54265c8fd4e /boot                   xfs     defaults        0 0
	#/dev/mapper/centos-swap swap                    swap    defaults        0 0
	[root@master mac]# 

### 关闭虚拟机


### 克隆虚拟机

	刷新所有网卡的MAC地址
	选择完全克隆的功能

	00:0C:29:85:33:28 （k8s_master）
	00:50:56:33:B4:E4 （k8s_node1）
	00:50:56:2A:D3:1C （k8s_node2）

### 为克隆的虚机修改主机名

	#hostnamectl --static set-hostname node1.k8s
	#hostnamectl --static set-hostname node2.k8s

### 查看各个虚机的IP地址

	[mac@node1 ~]$ ip a
	1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
	    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
	    inet 127.0.0.1/8 scope host lo
	       valid_lft forever preferred_lft forever
	    inet6 ::1/128 scope host 
	       valid_lft forever preferred_lft forever
	2: ens33: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc pfifo_fast state UP group default qlen 1000
	    link/ether 00:50:56:33:b4:e4 brd ff:ff:ff:ff:ff:ff
	    inet 192.168.0.107/24 brd 192.168.0.255 scope global noprefixroute dynamic ens33
	       valid_lft 4761sec preferred_lft 4761sec
	    inet6 fe80::ef57:d95e:5c18:b9c7/64 scope link tentative noprefixroute dadfailed 
	       valid_lft forever preferred_lft forever
	    inet6 fe80::f9e2:f92b:703f:20bf/64 scope link noprefixroute 

### 为三台主机配置名称解析

	[root@master mac]# vi /etc/hosts

	192.168.0.106 master.k8s
	192.168.0.107 node1.k8s
	192.168.0.108 node2.k8s

### 使用kubeadm列出需要的镜像

kubeadm默认会从k8s.gcr.io上下载kube的images，但是在国内环境是访问不了这些镜像的，所以可以从aliyun的registry上下载相应的image，然后修改tag，瞒过kubeadm。


	[root@master mac]# kubeadm config images list
	W0629 17:07:26.964486    8029 version.go:98] could not fetch a Kubernetes version from the internet: unable to get URL "https://dl.k8s.io/release/stable-1.txt": 
	Get https://dl.k8s.io/release/stable-1.txt: net/http: request canceled while waiting for connection (Client.Timeout exceeded while awaiting headers)
	W0629 17:07:26.964946    8029 version.go:99] falling back to the local client version: v1.15.0
	k8s.gcr.io/kube-apiserver:v1.15.0
	k8s.gcr.io/kube-controller-manager:v1.15.0
	k8s.gcr.io/kube-scheduler:v1.15.0
	k8s.gcr.io/kube-proxy:v1.15.0
	k8s.gcr.io/pause:3.1
	k8s.gcr.io/etcd:3.3.10
	k8s.gcr.io/coredns:1.3.1
	[root@master mac]# 

通过下面的方式(脚本)可以从阿里云的registry上下载镜像并修改tag:

	images=(
		kube-apiserver:v1.15.0
		kube-controller-manager:v1.15.0
		kube-scheduler:v1.15.0
		kube-proxy:v1.15.0
		pause:3.1
		etcd:3.3.10
		coredns:1.3.1
	)

	for imageName in ${images[@]} ; do
		docker pull registry.cn-hangzhou.aliyuncs.com/google_containers/$imageName
		docker tag registry.cn-hangzhou.aliyuncs.com/google_containers/$imageName k8s.gcr.io/$imageName
	done

如果你不嫌烦，可以手工下载并且修改镜像：

	docker pull registry.cn-hangzhou.aliyuncs.com/google_containers/kube-apiserver:v1.15.0
	docker pull registry.cn-hangzhou.aliyuncs.com/google_containers/kube-proxy:v1.15.0
	docker pull registry.cn-hangzhou.aliyuncs.com/google_containers/kube-scheduler:v1.15.0
	docker pull registry.cn-hangzhou.aliyuncs.com/google_containers/kube-controller-manager:v1.15.0
	docker pull registry.cn-hangzhou.aliyuncs.com/google_containers/coredns:1.3.1
	docker pull registry.cn-hangzhou.aliyuncs.com/google_containers/etcd:3.3.10
	docker pull registry.cn-hangzhou.aliyuncs.com/google_containers/pause:3.1

重新打成Google Containers的镜像标签

	docker tag registry.cn-hangzhou.aliyuncs.com/google_containers/kube-apiserver:v1.15.0 k8s.gcr.io/kube-apiserver:v1.15.0
	docker tag registry.cn-hangzhou.aliyuncs.com/google_containers/kube-controller-manager:v1.15.0 k8s.gcr.io/kube-controller-manager:v1.15.0
	docker tag registry.cn-hangzhou.aliyuncs.com/google_containers/kube-scheduler:v1.15.0 k8s.gcr.io/kube-scheduler:v1.15.0
	docker tag registry.cn-hangzhou.aliyuncs.com/google_containers/kube-proxy:v1.15.0 k8s.gcr.io/kube-proxy:v1.15.0
	docker tag registry.cn-hangzhou.aliyuncs.com/google_containers/pause:3.1 k8s.gcr.io/pause:3.1
	docker tag registry.cn-hangzhou.aliyuncs.com/google_containers/etcd:3.3.10 k8s.gcr.io/etcd:3.3.10
	docker tag registry.cn-hangzhou.aliyuncs.com/google_containers/coredns:1.3.1 k8s.gcr.io/coredns:1.3.1

删掉阿里云的镜像标签

	docker rmi registry.cn-hangzhou.aliyuncs.com/google_containers/kube-apiserver:v1.15.0
	docker rmi registry.cn-hangzhou.aliyuncs.com/google_containers/kube-proxy:v1.15.0
	docker rmi registry.cn-hangzhou.aliyuncs.com/google_containers/kube-scheduler:v1.15.0
	docker rmi registry.cn-hangzhou.aliyuncs.com/google_containers/kube-controller-manager:v1.15.0
	docker rmi registry.cn-hangzhou.aliyuncs.com/google_containers/coredns:1.3.1
	docker rmi registry.cn-hangzhou.aliyuncs.com/google_containers/etcd:3.3.10
	docker rmi registry.cn-hangzhou.aliyuncs.com/google_containers/pause:3.1


### 需要在其他节点上下载的镜像

我们需要在工作节点上提前从aliyun的registry上下载相应的image，然后修改tag，瞒过kubeadm/kubelet:

	docker pull registry.cn-hangzhou.aliyuncs.com/google_containers/kube-proxy:v1.15.0
	docker pull registry.cn-hangzhou.aliyuncs.com/google_containers/pause:3.1

重新打成Google Containers的镜像标签

	docker tag registry.cn-hangzhou.aliyuncs.com/google_containers/kube-proxy:v1.15.0 k8s.gcr.io/kube-proxy:v1.15.0
	docker tag registry.cn-hangzhou.aliyuncs.com/google_containers/pause:3.1 k8s.gcr.io/pause:3.1

删掉阿里云的镜像标签

	docker rmi registry.cn-hangzhou.aliyuncs.com/google_containers/kube-proxy:v1.15.0
	docker rmi registry.cn-hangzhou.aliyuncs.com/google_containers/pause:3.1


### 使用Kubeadm配置主节点

注意： 主节点需要设置成 **2 CPUs**。

	[root@master mac]# kubeadm init
	W0629 17:29:18.210598    7418 version.go:98] could not fetch a Kubernetes version from the internet: unable to get URL "https://dl.k8s.io/release/stable-1.txt": 
	Get https://dl.k8s.io/release/stable-1.txt: net/http: request canceled while waiting for connection (Client.Timeout exceeded while awaiting headers)
	W0629 17:29:18.211524    7418 version.go:99] falling back to the local client version: v1.15.0
	[init] Using Kubernetes version: v1.15.0
	[preflight] Running pre-flight checks
	[preflight] Pulling images required for setting up a Kubernetes cluster
	[preflight] This might take a minute or two, depending on the speed of your internet connection
	[preflight] You can also perform this action in beforehand using 'kubeadm config images pull'
	[kubelet-start] Writing kubelet environment file with flags to file "/var/lib/kubelet/kubeadm-flags.env"
	[kubelet-start] Writing kubelet configuration to file "/var/lib/kubelet/config.yaml"
	[kubelet-start] Activating the kubelet service
	[certs] Using certificateDir folder "/etc/kubernetes/pki"
	[certs] Generating "etcd/ca" certificate and key
	[certs] Generating "etcd/peer" certificate and key
	[certs] etcd/peer serving cert is signed for DNS names [master.k8s localhost] and IPs [192.168.0.106 127.0.0.1 ::1]
	[certs] Generating "apiserver-etcd-client" certificate and key
	[certs] Generating "etcd/server" certificate and key
	[certs] etcd/server serving cert is signed for DNS names [master.k8s localhost] and IPs [192.168.0.106 127.0.0.1 ::1]
	[certs] Generating "etcd/healthcheck-client" certificate and key
	[certs] Generating "front-proxy-ca" certificate and key
	[certs] Generating "front-proxy-client" certificate and key
	[certs] Generating "ca" certificate and key
	[certs] Generating "apiserver" certificate and key
	[certs] apiserver serving cert is signed for DNS names [master.k8s kubernetes kubernetes.default kubernetes.default.svc kubernetes.default.svc.cluster.local] and IPs [10.96.0.1 192.168.0.106]
	[certs] Generating "apiserver-kubelet-client" certificate and key
	[certs] Generating "sa" key and public key
	[kubeconfig] Using kubeconfig folder "/etc/kubernetes"
	[kubeconfig] Writing "admin.conf" kubeconfig file
	[kubeconfig] Writing "kubelet.conf" kubeconfig file
	[kubeconfig] Writing "controller-manager.conf" kubeconfig file
	[kubeconfig] Writing "scheduler.conf" kubeconfig file
	[control-plane] Using manifest folder "/etc/kubernetes/manifests"
	[control-plane] Creating static Pod manifest for "kube-apiserver"
	[control-plane] Creating static Pod manifest for "kube-controller-manager"
	[control-plane] Creating static Pod manifest for "kube-scheduler"
	[etcd] Creating static Pod manifest for local etcd in "/etc/kubernetes/manifests"
	[wait-control-plane] Waiting for the kubelet to boot up the control plane as static Pods from directory "/etc/kubernetes/manifests". This can take up to 4m0s
	[apiclient] All control plane components are healthy after 39.005987 seconds
	[upload-config] Storing the configuration used in ConfigMap "kubeadm-config" in the "kube-system" Namespace
	[kubelet] Creating a ConfigMap "kubelet-config-1.15" in namespace kube-system with the configuration for the kubelets in the cluster
	[upload-certs] Skipping phase. Please see --upload-certs
	[mark-control-plane] Marking the node master.k8s as control-plane by adding the label "node-role.kubernetes.io/master=''"
	[mark-control-plane] Marking the node master.k8s as control-plane by adding the taints [node-role.kubernetes.io/master:NoSchedule]
	[kubelet-check] Initial timeout of 40s passed.
	[bootstrap-token] Using token: 640q11.ed4t8j2g3gjzd0pt
	[bootstrap-token] Configuring bootstrap tokens, cluster-info ConfigMap, RBAC Roles
	[bootstrap-token] configured RBAC rules to allow Node Bootstrap tokens to post CSRs in order for nodes to get long term certificate credentials
	[bootstrap-token] configured RBAC rules to allow the csrapprover controller automatically approve CSRs from a Node Bootstrap Token
	[bootstrap-token] configured RBAC rules to allow certificate rotation for all node client certificates in the cluster
	[bootstrap-token] Creating the "cluster-info" ConfigMap in the "kube-public" namespace
	[addons] Applied essential addon: CoreDNS
	[addons] Applied essential addon: kube-proxy
	
	Your Kubernetes control-plane has initialized successfully!
	
	To start using your cluster, you need to run the following as a regular user:
	
	  mkdir -p $HOME/.kube
	  sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
	  sudo chown $(id -u):$(id -g) $HOME/.kube/config
	
	You should now deploy a pod network to the cluster.
	Run "kubectl apply -f [podnetwork].yaml" with one of the options listed at:
	  https://kubernetes.io/docs/concepts/cluster-administration/addons/
	
	Then you can join any number of worker nodes by running the following on each as root:
	
	kubeadm join 192.168.0.106:6443 --token 640q11.ed4t8j2g3gjzd0pt \
	    --discovery-token-ca-cert-hash sha256:6df987ff144ea7f443e6062a3f0a46c21de02c8a79c016d7100ad9469ba0c6be 
	[root@master mac]# 

另外，需要记录好kubeadm init命令输出的最后一段内容，后续过程需要用到它。

### 在主节点上运行 kubectl

在初始化步骤中安装了kubectl，以及docker、kubeadm和其他软件包。但是，在配置过kubeconfig文件之前，无法使用kubectl与集群进行通信。

需要使用 /etc/kubernetes/admin.conf ：

	[root@master mac]# export KUBECONFIG=/etc/kubernetes/admin.conf 
	[root@master mac]# 

下面列出此文件的内容：

	[root@master mac]# cat /etc/kubernetes/admin.conf 
	apiVersion: v1
	clusters:
	- cluster:
	    certificate-authority-data: LS0tLS1CRUdJTiBDRVJUSUZJQ0FURS0tLS0tCk1JSUN5RENDQWJDZ0F3SUJBZ0lCQURBTkJna3Foa2lHOXcwQkFRc0ZBREFWTVJNd0VRWURWUVFERXdwcmRXSmwKY201bGRHVnpNQjRYRFRFNU1EWXlPVEE1TWpreU1Gb1hEVEk1TURZeU5qQTVNamt5TUZvd0ZURVRNQkVHQTFVRQpBeE1LYTNWaVpYSnVaWFJsY3pDQ0FTSXdEUVlKS29aSWh2Y05BUUVCQlFBRGdnRVBBRENDQVFvQ2dnRUJBTHlSCjlIR1ZYTEN3dXhiekdOWERJeHdraVorL05NK2pLMjlZb1FQNVNVUVlPeEdzMDZsZ0dMYUx0bGRHSVFkaXRtYi8KQ3JYbFl1TnZrSjUrR2FucmFMK3FjQXJJTnV3d0w5d29vREg3aE9Nb0kvSk94NHZvbFRGMFluMytWbmt2OUU1VwpnaEt6N3p0eklEMkNXMmNJZSs3WS9QWDZKTG9FYndsTW04d2V0c0lJN2dPaGp1c3RoSHBwY0V1M0hRMndXSWxiCjJ0SW1DWksxWmpJcU40aHJmWlg5N0Z6aWxwSldIeklvTmdnWWtRalZOb3ZIM2hXRUtYN04yNTFGeTJOekNVcG0KSmE4Q3BieUNGdXAyTTliYjZOamVBNnNONU1ySG40Q0FKTlcxci9ocGRRenJyVkZ2b25nY05GMyt0SUM3NkdsdApCRjVlSnd5Vy9tb08yMlN2bmZNQ0F3RUFBYU1qTUNFd0RnWURWUjBQQVFIL0JBUURBZ0trTUE4R0ExVWRFd0VCCi93UUZNQU1CQWY4d0RRWUpLb1pJaHZjTkFRRUxCUUFEZ2dFQkFKcld0UEpIMEkzYUxKYWtmOTkvdG5qWnU4dWYKZlVRQm41dVQwWXZYWFByN0hBZGpubVI2L21PSEMzMHNqc0MxbGU3SDdjWjZQcXJiYlREcXlNV09iN1ArTC8rbwptUzZqcHFjVFlQeFM5Z21hZ0ZqTlFlcEtZZWhGL3dBQlo4eGlINTI0YzF0dFRTWms3WVpMU09LR2FlL3JXU3VLCnpFZG9hNmFmaWFDMWozOXIrOHZPbHk2UmRvRmR5RGhhWFNsamZZejZvY29SYTh4emJ6b0FHWGRMQXhZUjVPbHcKSmo1R3pHU2grQXNMZ3RSSklHNFZJUVBpTzJqaFFlVlVyaCt5MFBnTjlLUzJOUGdiTjdNZXJiRE1ZdmZMY2ltYwpIaDdwRjN6M1U5aXlXZG40TE10QUJkcTN5RWdJSzdYWFhCY0trWTlWVnBXblQyYU5WT2tGSmRTVU1BWT0KLS0tLS1FTkQgQ0VSVElGSUNBVEUtLS0tLQo=
	    server: https://192.168.0.106:6443
	  name: kubernetes
	contexts:
	- context:
	    cluster: kubernetes
	    user: kubernetes-admin
	  name: kubernetes-admin@kubernetes
	current-context: kubernetes-admin@kubernetes
	kind: Config
	preferences: {}
	users:
	- name: kubernetes-admin
	  user:
	    client-certificate-data: LS0tLS1CRUdJTiBDRVJUSUZJQ0FURS0tLS0tCk1JSUM4akNDQWRxZ0F3SUJBZ0lJQ2UxU3NNdnZRaUl3RFFZSktvWklodmNOQVFFTEJRQXdGVEVUTUJFR0ExVUUKQXhNS2EzVmlaWEp1WlhSbGN6QWVGdzB4T1RBMk1qa3dPVEk1TWpCYUZ3MHlNREEyTWpnd09USTVNakZhTURReApGekFWQmdOVkJBb1REbk41YzNSbGJUcHRZWE4wWlhKek1Sa3dGd1lEVlFRREV4QnJkV0psY201bGRHVnpMV0ZrCmJXbHVNSUlCSWpBTkJna3Foa2lHOXcwQkFRRUZBQU9DQVE4QU1JSUJDZ0tDQVFFQXZ5MzladzQ1MGNYSVEyemcKbDFZK09qU3FZZXkwWnBGakF6aWRnUHBZSExJSTM1b1M5VVd4Z1FqTjZXb0s0RHQ3NlR5SGhkZXJlWkdJZjMzaApMTVgybGZUbXk4NXQ0K09UUHR2Qlp6ZU45OURFdExDSjlJWjlPY3VJTTNwTnBBZHNicnNDOTZJeWJTZHFnUG94CmJ3WitXRmU5eEhObUpRQWxtME9mOUo2SGQ1S25aVzU3M21hdXZ5OWoyQ2NZVzlWRndlV2JLZDV5aUZhbmpPc08KK045aWtKdE40NlN6eTZ0ZjNqbitqWGxUSXdTY08yb05XZUg4d2VIVjkyWjh5aVhjWFQ4RTc2TWJ5bXFJK295QQpVTk5RM1hYMnBOZTJ2UFdGV0N5YitTNDJrRnNkYmlXMS92RitLdzFSaThBVm1qOWtmakpudHdwS3R6RElYemdpCjdRbVNKUUlEQVFBQm95Y3dKVEFPQmdOVkhROEJBZjhFQkFNQ0JhQXdFd1lEVlIwbEJBd3dDZ1lJS3dZQkJRVUgKQXdJd0RRWUpLb1pJaHZjTkFRRUxCUUFEZ2dFQkFJdmlmak04SThCRE15ZjNKRFZaSmhYY0NYOWNqZnFreVZxZQpKR29tTjZ3aDFLOGR5VEF1bVhlSVZwNGRTZHpjMDBHSlhsRTg1a2ttaXYybkJ4aDZZTTB0dTRUaHNHd2hTU0I2ClM1Q1ZyMEE1eUkwNXdvSlNVclM3dEVvbEJYK3o3Kyt5bXpCYTBTWThDVm9vS3ZNc1Z0UzdKUDBEMEZWem5QMHYKbERQM2ljRTlrT3lwUkl5Q0RlRlZOQWRXWUthNjBDY3YrK054dnFHc1FCZ3lsUDJUazRGWTJwTmFwY2hPM0htUQo3SUhPbjVsQ3lYdkhuMVB5cURQZXFqekFrWEV4TVA1d1B3cXY5K29mVWJpSDRaejJHaE54Y0UxdEFHTDBoQnFvCi9laHMvMmFKTWQ5VGl0WDZaUGoyaU0zUEp4THB2VGUwRkcra2ZPRkhLT2thSzFnQzdNND0KLS0tLS1FTkQgQ0VSVElGSUNBVEUtLS0tLQo=
	    client-key-data: LS0tLS1CRUdJTiBSU0EgUFJJVkFURSBLRVktLS0tLQpNSUlFcFFJQkFBS0NBUUVBdnkzOVp3NDUwY1hJUTJ6Z2wxWStPalNxWWV5MFpwRmpBemlkZ1BwWUhMSUkzNW9TCjlVV3hnUWpONldvSzREdDc2VHlIaGRlcmVaR0lmMzNoTE1YMmxmVG15ODV0NCtPVFB0dkJaemVOOTlERXRMQ0oKOUlaOU9jdUlNM3BOcEFkc2Jyc0M5Nkl5YlNkcWdQb3hid1orV0ZlOXhITm1KUUFsbTBPZjlKNkhkNUtuWlc1NwozbWF1dnk5ajJDY1lXOVZGd2VXYktkNXlpRmFuak9zTytOOWlrSnRONDZTenk2dGYzam4ralhsVEl3U2NPMm9OCldlSDh3ZUhWOTJaOHlpWGNYVDhFNzZNYnltcUkrb3lBVU5OUTNYWDJwTmUydlBXRldDeWIrUzQya0ZzZGJpVzEKL3ZGK0t3MVJpOEFWbWo5a2ZqSm50d3BLdHpESVh6Z2k3UW1TSlFJREFRQUJBb0lCQVFDN3ZrYzJ1REt4dmFBdwpEckQwRFg2b25HV2lLdGp5VE41R0lJZ1VURVRSVVVrRGhRUVBGL1Q3K1pCMUkyMHd6Vm1mTDVFTE1FTzE2K1IzCkIwQmxQcmNzaGtkTWFCbGtqVzFoY2wrWXBHYm5zWDRxejU5Nm9jUkNTSTBsdUhxY2xhbTNpREdlekFyblJLa0QKcGk5N2o0M3Q1YVIzVXJoQnA4Wkdsbjl6czJiblZVdUloVnpJTkx4R3FJL1ZwRUV3djF1eERPU0tJdG85QW1vYQoxRWovME5xQkR4TDdScGFyVkhXQzhkUGtZZ2NVOXJNZU9NTXViR3lEY2JVYllZdlU0UHJVZ2VpNG03SU5oZnhzCnc4eTV6dWpQSENXdG84UFdxekJBVENPaVJFMEY1VVhaMmsrSHZLMUpxRTB1UUIydHM3MXZlTkhyd05aOWg5RU8KNG5JT04remhBb0dCQU5DUWFJTEREMjFDVWo4RFN4S3pJRzhrUWY0RU5Eb3pZUmV5SHpBVWpnUmZoejZLeW9ySApJeTZKODVvUHRIeXZPbjNLa05jQjBYbENoeVJKOVhDaVpodUdPdkJxdVpwOEVlY1JQeHhXcFNEOGFxWEtFdEJZCjZwSWFvOUh0akRNcUJhRXFtWDFHSllTL3RlSjFTdVNtMmV3bm44OEdkT0pwS1JtNytzR3p5Q0taQW9HQkFPcXAKWUdlVHJQODJ4QVRTZlFnWDVZRHNQbTFWMERLUWxRanhSZEc5d1RjYmVDRmxmSzVKVm1pWStlc05PSFdUWktQTApDUHFOL05RTjI2Z05HQ3hVUDRpZkRnMGljVnhDem9vTzRmSi8xeEsrRUlrUWFobHhWQUV6T3dhVmtEeGdGMzE4CkNNUHkzY0FmbElVYUhydURwVUo3d1VyOXg1R3Y3SFRmOXhJR2R1OXRBb0dCQU1MRDZHVWNaVDZoN1k1Y3MvRzkKaDI5aXk2RzhLVTJraDJvS2MrZUJlbklKQjVKWEovZmJLVGFmcXZaVzdqUjFxc2lucndTcDlRVXBKR3kyQ0Zkcgp3TEM1ZERicFkzUXBvc3BHcDhuOSsrekc2NHp4SFFxbHprQXNVb21MTFI3bWdpVlVVOHZTQXQxcDdoK1JheVFGCjBJSWhLcks1RTlRUFlrdGU2VGVVZlRRWkFvR0JBTEV2bFhDQURGZGt0ZHZpUjdCdHdzaDNHYWdhN0tyUml3Y0cKank2UTlpeXpIQ0V6YlZKNFk3dDFEdmhSc2pqdFEwZCtEbGlLRDhiYWMrcFBnTm92L3cwYzlGSXNtS1lPZDcrOAoveFRKUE0rVkhnMHdqTHlMV3QvUkhCZWJwUjVCZkZzdTVidDNUY004MVRzdmZ0Y2R6eElGT2UxeTlGYm9IRVlmCnVvSXN5Vzk5QW9HQVFMNm9pdVdzRlBHajMrZU9rNkE5RFNrYzc2SWRYczkrRHRtMjU0TG1HaHhqVDhSVmx5S1YKU015ejZzWHlXMHZWR0Y1NlBScUNyeCtGNE5rNENqWmtpQ1F3YnhVZ0dGN29iWmxFYjR1TUVubU9QWXJFVlRpRQpjVDJoM3JMK3M1UDBGQjNCWEI4anBKdEhKenA4U2lDdUt6WlJTN2d6dFZ0a0w4MEFwUkFZS1dnPQotLS0tLUVORCBSU0EgUFJJVkFURSBLRVktLS0tLQo=
	[root@master mac]# 

当设置了KUBECONFFIG 系统参数后，就可以与集群进行通信了，试着 检查一下 K8S的下列资源吧。

	[root@master mac]# kubectl get pods
	No resources found.
	[root@master mac]# 

	[root@master mac]# kubectl get nodes
	NAME         STATUS     ROLES    AGE    VERSION
	master.k8s   NotReady   master   5m1s   v1.15.0
	[root@master mac]# 

	[root@master mac]# kubectl get pod -n kube-system
	NAME                                 READY   STATUS    RESTARTS   AGE
	coredns-5c98db65d4-62fl4             0/1     Running   0          5m7s
	coredns-5c98db65d4-fq4n9             0/1     Running   0          5m7s
	etcd-master.k8s                      1/1     Running   0          4m15s
	kube-apiserver-master.k8s            1/1     Running   0          4m8s
	kube-controller-manager-master.k8s   1/1     Running   0          4m14s
	kube-proxy-p2m6r                     1/1     Running   0          5m7s
	kube-scheduler-master.k8s            1/1     Running   0          4m20s
	[root@master mac]# 

	[root@master mac]# kubectl get services
	NAME         TYPE        CLUSTER-IP   EXTERNAL-IP   PORT(S)   AGE
	kubernetes   ClusterIP   10.96.0.1    <none>        443/TCP   6m2s
	[root@master mac]# 

	[root@master mac]# kubectl cluster-info
	Kubernetes master is running at https://192.168.0.106:6443
	KubeDNS is running at https://192.168.0.106:6443/api/v1/namespaces/kube-system/services/kube-dns:dns/proxy
	To further debug and diagnose cluster problems, use 'kubectl cluster-info dump'.
	[root@master mac]# 

可以看到目前仅仅是主节点，而且状态是NotReady，我们需要先配置另外两个节点。

### 加入主节点

在node1和node2上执行如下的命令：

	[root@node1 mac]# kubeadm join 192.168.0.106:6443 --token 640q11.ed4t8j2g3gjzd0pt \
	>     --discovery-token-ca-cert-hash sha256:6df987ff144ea7f443e6062a3f0a46c21de02c8a79c016d7100ad9469ba0c6be 
	[preflight] Running pre-flight checks
	[preflight] Reading configuration from the cluster...
	[preflight] FYI: You can look at this config file with 'kubectl -n kube-system get cm kubeadm-config -oyaml'
	[kubelet-start] Downloading configuration for the kubelet from the "kubelet-config-1.15" ConfigMap in the kube-system namespace
	[kubelet-start] Writing kubelet configuration to file "/var/lib/kubelet/config.yaml"
	[kubelet-start] Writing kubelet environment file with flags to file "/var/lib/kubelet/kubeadm-flags.env"
	[kubelet-start] Activating the kubelet service
	[kubelet-start] Waiting for the kubelet to perform the TLS Bootstrap...
	
	This node has joined the cluster:
	* Certificate signing request was sent to apiserver and a response was received.
	* The Kubelet was informed of the new secure connection details.
	
	Run 'kubectl get nodes' on the control-plane to see this node join the cluster.
	
	[root@node1 mac]# 

返回主节点，运行如下的命令：

	[root@master mac]# kubectl get nodes
	NAME         STATUS     ROLES    AGE    VERSION
	master.k8s   NotReady   master   12m    v1.15.0
	node1.k8s    NotReady   <none>   118s   v1.15.0
	node2.k8s    NotReady   <none>   28s    v1.15.0
	[root@master mac]# 

使用以下的命令，查看node状态的具体原因：

	[root@master mac]# kubectl describe node node1.k8s
	Name:               node1.k8s
	Roles:              <none>
	Labels:             beta.kubernetes.io/arch=amd64
	                    beta.kubernetes.io/os=linux
	                    kubernetes.io/arch=amd64
	                    kubernetes.io/hostname=node1.k8s
	                    kubernetes.io/os=linux
	Annotations:        kubeadm.alpha.kubernetes.io/cri-socket: /var/run/dockershim.sock
	                    node.alpha.kubernetes.io/ttl: 0
	                    volumes.kubernetes.io/controller-managed-attach-detach: true
	CreationTimestamp:  Sat, 29 Jun 2019 17:40:51 +0800
	Taints:             node.kubernetes.io/not-ready:NoSchedule
	Unschedulable:      false
	Conditions:
	  Type             Status  LastHeartbeatTime                 LastTransitionTime                Reason                       Message
	  ----             ------  -----------------                 ------------------                ------                       -------
	  MemoryPressure   False   Sat, 29 Jun 2019 17:44:00 +0800   Sat, 29 Jun 2019 17:40:50 +0800   KubeletHasSufficientMemory   kubelet has sufficient memory available
	  DiskPressure     False   Sat, 29 Jun 2019 17:44:00 +0800   Sat, 29 Jun 2019 17:40:50 +0800   KubeletHasNoDiskPressure     kubelet has no disk pressure
	  PIDPressure      False   Sat, 29 Jun 2019 17:44:00 +0800   Sat, 29 Jun 2019 17:40:50 +0800   KubeletHasSufficientPID      kubelet has sufficient PID available
	  Ready            False   Sat, 29 Jun 2019 17:44:00 +0800   Sat, 29 Jun 2019 17:40:50 +0800   KubeletNotReady              runtime network not ready: NetworkReady=false reason:NetworkPluginNotReady message:docker: network plugin is not ready: cni config uninitialized
	Addresses:
	  InternalIP:  192.168.0.107
	  Hostname:    node1.k8s
	Capacity:
	 cpu:                1
	 ephemeral-storage:  17394Mi
	 hugepages-1Gi:      0
	 hugepages-2Mi:      0
	 memory:             995892Ki
	 pods:               110
	Allocatable:
	 cpu:                1
	 ephemeral-storage:  16415037823
	 hugepages-1Gi:      0
	 hugepages-2Mi:      0
	 memory:             893492Ki
	 pods:               110
	System Info:
	 Machine ID:                 90c007df13bc49d6b8be8742c0d30617
	 System UUID:                08224D56-30F4-6D4C-F7F5-AA98A44DA407
	 Boot ID:                    811c3f40-864b-472d-95dd-fa2379d3e54d
	 Kernel Version:             3.10.0-957.21.3.el7.x86_64
	 OS Image:                   CentOS Linux 7 (Core)
	 Operating System:           linux
	 Architecture:               amd64
	 Container Runtime Version:  docker://1.13.1
	 Kubelet Version:            v1.15.0
	 Kube-Proxy Version:         v1.15.0
	Non-terminated Pods:         (1 in total)
	  Namespace                  Name                CPU Requests  CPU Limits  Memory Requests  Memory Limits  AGE
	  ---------                  ----                ------------  ----------  ---------------  -------------  ---
	  kube-system                kube-proxy-bq4jn    0 (0%)        0 (0%)      0 (0%)           0 (0%)         3m49s
	Allocated resources:
	  (Total limits may be over 100 percent, i.e., overcommitted.)
	  Resource           Requests  Limits
	  --------           --------  ------
	  cpu                0 (0%)    0 (0%)
	  memory             0 (0%)    0 (0%)
	  ephemeral-storage  0 (0%)    0 (0%)
	Events:
	  Type    Reason                   Age                    From                Message
	  ----    ------                   ----                   ----                -------
	  Normal  Starting                 3m50s                  kubelet, node1.k8s  Starting kubelet.
	  Normal  NodeHasSufficientMemory  3m50s (x2 over 3m50s)  kubelet, node1.k8s  Node node1.k8s status is now: NodeHasSufficientMemory
	  Normal  NodeHasNoDiskPressure    3m50s (x2 over 3m50s)  kubelet, node1.k8s  Node node1.k8s status is now: NodeHasNoDiskPressure
	  Normal  NodeHasSufficientPID     3m50s (x2 over 3m50s)  kubelet, node1.k8s  Node node1.k8s status is now: NodeHasSufficientPID
	  Normal  NodeAllocatableEnforced  3m50s                  kubelet, node1.k8s  Updated Node Allocatable limit across pods
	[root@master mac]# 

### 配置容器网络

通过查看上面的文字，可以得知：runtime network not ready: NetworkReady=false reason:NetworkPluginNotReady message:docker: network plugin is not ready: **cni config uninitialized**

因为容器网络（CNI）插件没有准备好，所以Node状态为NotReady。

	[root@master mac]# kubectl apply -f "https://cloud.weave.works/k8s/net?k8s-version=$(kubectl version | base64 | tr -d '\n')"
	serviceaccount/weave-net created
	clusterrole.rbac.authorization.k8s.io/weave-net created
	clusterrolebinding.rbac.authorization.k8s.io/weave-net created
	role.rbac.authorization.k8s.io/weave-net created
	rolebinding.rbac.authorization.k8s.io/weave-net created
	daemonset.extensions/weave-net created
	[root@master mac]# 

上面的kubectl apply 部署了一个DaemonSet和一些与安全相关的资源，一个DaemonSet控制器会创建一个Pod副本，并且在所有的节点上启动，从而节点的状态变成了Ready。

	[root@master mac]# kubectl get nodes
	NAME         STATUS   ROLES    AGE     VERSION
	master.k8s   Ready    master   19h   v1.15.0
	node1.k8s    Ready    <none>   19h   v1.15.0
	node2.k8s    Ready    <none>   19h   v1.15.0
	[root@master mac]# 

查看Nodes具体信息：

	[root@master mac]# kubectl get nodes -o wide
	NAME         STATUS   ROLES    AGE     VERSION   INTERNAL-IP     EXTERNAL-IP   OS-IMAGE                KERNEL-VERSION               CONTAINER-RUNTIME
	master.k8s   Ready    master   4d19h   v1.15.0   192.168.0.106   <none>        CentOS Linux 7 (Core)   3.10.0-957.21.3.el7.x86_64   docker://1.13.1
	node1.k8s    Ready    <none>   4d19h   v1.15.0   192.168.0.107   <none>        CentOS Linux 7 (Core)   3.10.0-957.21.3.el7.x86_64   docker://1.13.1
	node2.k8s    Ready    <none>   4d19h   v1.15.0   192.168.0.108   <none>        CentOS Linux 7 (Core)   3.10.0-957.21.3.el7.x86_64   docker://1.13.1
	[root@master mac]# 

查看Pods

	[root@master mac]# kubectl get po --all-namespaces
	NAMESPACE     NAME                                 READY   STATUS    RESTARTS   AGE
	kube-system   coredns-5c98db65d4-62fl4             1/1     Running   3          19h
	kube-system   coredns-5c98db65d4-fq4n9             1/1     Running   3          19h
	kube-system   etcd-master.k8s                      1/1     Running   5          19h
	kube-system   kube-apiserver-master.k8s            1/1     Running   5          19h
	kube-system   kube-controller-manager-master.k8s   1/1     Running   5          19h
	kube-system   kube-proxy-bq4jn                     1/1     Running   3          19h
	kube-system   kube-proxy-d27gg                     1/1     Running   4          19h
	kube-system   kube-proxy-p2m6r                     1/1     Running   5          19h
	kube-system   kube-scheduler-master.k8s            1/1     Running   5          19h
	kube-system   weave-net-6kf5m                      2/2     Running   21         20h
	kube-system   weave-net-9m7lb                      2/2     Running   9          20h
	kube-system   weave-net-k74b2                      2/2     Running   19         20h
	[root@master mac]# 


### 在本地使用集群

对于普通用户，你可以这样操作：

	To start using your cluster, you need to run the following as a regular user:
	
	  mkdir -p $HOME/.kube
	  sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
	  sudo chown $(id -u):$(id -g) $HOME/.kube/config


你可以使用下面的操作，在本地机器上使用集群：

	cd
	mkdir -p $HOME/.kube
	mkdir -p $HOME/.kube/config
	scp root@192.168.0.106:/etc/kubernetes/admin.conf ~/.kube/config/
	sudo chown $(id -u):$(id -g) $HOME/.kube/config
	$export KUBECONFIG=~/.kube/config/admin.conf
	or edit .bash_profile, add the line:
	export KUBECONFIG=~/.kube/config/admin.conf


### 在另外一台物理机上

之前的Token已经失效，所以重新生成：

	[root@master demo_k8s]# kubeadm token create
	tl6prz.3lmof380fowwkmxf
	[root@master demo_k8s]# 
	[root@master demo_k8s]# kubeadm token list
	TOKEN                     TTL       EXPIRES                     USAGES                   DESCRIPTION   EXTRA GROUPS
	tl6prz.3lmof380fowwkmxf   23h       2019-07-06T19:17:35+08:00   authentication,signing   <none>        system:bootstrappers:kubeadm:default-node-token
	[root@master demo_k8s]# 

修改 kubeadm join串： tl6prz.3lmof380fowwkmxf 是新的串

	kubeadm join 192.168.0.106:6443 --token tl6prz.3lmof380fowwkmxf --discovery-token-ca-cert-hash sha256:6df987ff144ea7f443e6062a3f0a46c21de02c8a79c016d7100ad9469ba0c6be

在新的物理机（或者虚拟机上）执行：

	[root@node3 mac]# kubeadm join 192.168.0.106:6443 --token 640q11.ed4t8j2g3gjzd0pt --discovery-token-ca-cert-hash sha256:6df987ff144ea7f443e6062a3f0a46c21de02c8a79c016d7100ad9469ba0c6be
	[preflight] Running pre-flight checks
	error execution phase preflight: couldn't validate the identity of the API Server: abort connecting to API servers after timeout of 5m0s
	[root@node3 mac]# 
	[root@node3 mac]# 
	[root@node3 mac]# 
	[root@node3 mac]# kubeadm join 192.168.0.106:6443 --token tl6prz.3lmof380fowwkmxf
	discovery.bootstrapToken: Invalid value: "": using token-based discovery without caCertHashes can be unsafe. Set unsafeSkipCAVerification as true in your kubeadm config file or pass --discovery-token-unsafe-skip-ca-verification flag to continue
	[root@node3 mac]# 
	[root@node3 mac]# kubeadm join 192.168.0.106:6443 --token tl6prz.3lmof380fowwkmxf --discovery-token-ca-cert-hash sha256:6df987ff144ea7f443e6062a3f0a46c21de02c8a79c016d7100ad9469ba0c6be
	[preflight] Running pre-flight checks
	[preflight] Reading configuration from the cluster...
	[preflight] FYI: You can look at this config file with 'kubectl -n kube-system get cm kubeadm-config -oyaml'
	[kubelet-start] Downloading configuration for the kubelet from the "kubelet-config-1.15" ConfigMap in the kube-system namespace
	[kubelet-start] Writing kubelet configuration to file "/var/lib/kubelet/config.yaml"
	[kubelet-start] Writing kubelet environment file with flags to file "/var/lib/kubelet/kubeadm-flags.env"
	[kubelet-start] Activating the kubelet service
	[kubelet-start] Waiting for the kubelet to perform the TLS Bootstrap...
	
	This node has joined the cluster:
	* Certificate signing request was sent to apiserver and a response was received.
	* The Kubelet was informed of the new secure connection details.
	
	Run 'kubectl get nodes' on the control-plane to see this node join the cluster.
	
	[root@node3 mac]# 

返回主节点，检查node状态：

	[root@master demo_k8s]# kubectl get nodes
	NAME         STATUS   ROLES    AGE    VERSION
	master.k8s   Ready    master   6d1h   v1.15.0
	node1.k8s    Ready    <none>   6d1h   v1.15.0
	node2.k8s    Ready    <none>   6d1h   v1.15.0
	node3.k8s    Ready    <none>   2m8s   v1.15.0
	[root@master demo_k8s]# 

返回新的节点，查看Docker 状态：

	[root@node3 mac]# docker images
	REPOSITORY                                                       TAG                 IMAGE ID            CREATED             SIZE
	registry.cn-hangzhou.aliyuncs.com/google_containers/kube-proxy   v1.15.0             d235b23c3570        2 weeks ago         82.4 MB
	registry.cn-hangzhou.aliyuncs.com/google_containers/pause        3.1                 da86e6ba6ca1        18 months ago       742 kB
	k8s.gcr.io/kube-proxy                                            v1.15.0             d235b23c3570        2 weeks ago         82.4 MB
	k8s.gcr.io/pause                                                 3.1                 da86e6ba6ca1        18 months ago       742 kB
	docker.io/weaveworks/weave-kube                                  2.5.2               f04a043bb67a        7 weeks ago         148 MB
	docker.io/weaveworks/weave-npc                                   2.5.2               5ce48e0d813c        7 weeks ago         49.6 MB
	docker.io/busybox                                                latest              e4db68de4ff2        2 weeks ago         1.22 MB
	[root@node3 mac]# 


## 08 K8S架构

### Master节点


### Node 节点


### 完整架构图

K8S coredns 提供DNS服务
 	
	[root@master mac]# kubectl get pods --all-namespaces
	NAMESPACE     NAME                                   READY   STATUS    RESTARTS   AGE
	default       kubernetes-bootcamp-7dc9765bf6-hvh6k   1/1     Running   0          74m
	default       kubernetes-bootcamp-7dc9765bf6-pnh6s   1/1     Running   0          75m
	kube-system   coredns-5c98db65d4-62fl4               1/1     Running   2          4d2h
	kube-system   coredns-5c98db65d4-fq4n9               1/1     Running   2          4d2h
	kube-system   etcd-master.k8s                        1/1     Running   4          4d2h
	kube-system   kube-apiserver-master.k8s              1/1     Running   4          4d2h
	kube-system   kube-controller-manager-master.k8s     1/1     Running   4          4d2h
	kube-system   kube-proxy-bq4jn                       1/1     Running   2          4d2h
	kube-system   kube-proxy-d27gg                       1/1     Running   2          4d2h
	kube-system   kube-proxy-p2m6r                       1/1     Running   4          4d2h
	kube-system   kube-scheduler-master.k8s              1/1     Running   4          4d2h
	kube-system   weave-net-6kf5m                        2/2     Running   15         3d3h
	kube-system   weave-net-9m7lb                        2/2     Running   6          3d3h
	kube-system   weave-net-k74b2                        2/2     Running   16         3d3h
	[root@master mac]# 

kubelet是唯一没有以容器形式运行的组件。

### 用一个例子把它们串起来

查看Httpd镜像： https://hub.docker.com/_/httpd

	[root@master mac]# docker search httpd
	INDEX       NAME                                           DESCRIPTION                                     STARS     OFFICIAL   AUTOMATED
	docker.io   docker.io/httpd                                The Apache HTTP Server Project                  2537      [OK]       
	docker.io   docker.io/centos/httpd                                                                         23                   [OK]

获取Httpd镜像：

	[root@master mac]# docker pull httpd
	Using default tag: latest
	Trying to pull repository docker.io/library/httpd ... 
	latest: Pulling from docker.io/library/httpd
	fc7181108d40: Pull complete 
	b183a5e3b6da: Pull complete 
	c52952f0d826: Pull complete 
	c8f255a56e9a: Pull complete 
	144c3b858b48: Pull complete 
	Digest: sha256:a129c3a747fe9e406bf91d4d1fb2d4ed7b51d7a1f523fcf372c18c3c35981d12
	Status: Downloaded newer image for docker.io/httpd:latest
	[root@master mac]# 

部署Httpd应用：

	[root@master mac]# kubectl run httpd-app --image=httpd --replicas=2
	kubectl run --generator=deployment/apps.v1 is DEPRECATED and will be removed in a future version. Use kubectl run --generator=run-pod/v1 or kubectl create instead.
	deployment.apps/httpd-app created
	[root@master mac]# 

查看部署：

	[root@master mac]# kubectl get deployments
	NAME                  READY   UP-TO-DATE   AVAILABLE   AGE
	httpd-app             0/2     2            0           8s
	kubernetes-bootcamp   2/2     2            2           130m
	[root@master mac]# 
	[root@master mac]# kubectl get pods
	NAME                                   READY   STATUS              RESTARTS   AGE
	httpd-app-5bc589d9f7-hds8g             0/1     ContainerCreating   0          21s
	httpd-app-5bc589d9f7-v45nw             0/1     ContainerCreating   0          21s
	[root@master mac]# 

	[root@master mac]# kubectl get pods -o wide
	NAME                                   READY   STATUS    RESTARTS   AGE     IP          NODE        NOMINATED NODE   READINESS GATES
	httpd-app-5bc589d9f7-hds8g             1/1     Running   0          2m48s   10.32.0.2   node2.k8s   <none>           <none>
	httpd-app-5bc589d9f7-v45nw             1/1     Running   0          2m48s   10.38.0.2   node1.k8s   <none>           <none>
	[root@master mac]# 

测试应用：

	[root@master mac]# curl 10.32.0.2
	<html><body><h1>It works!</h1></body></html>
	[root@master mac]# 
	[root@master mac]# curl 10.38.0.2
	<html><body><h1>It works!</h1></body></html>
	[root@master mac]# 

## 09 运行应用

### Deployment

#### 准备Nginx镜像

	https://hub.docker.com/_/nginx
	
	[root@master mac]# docker pull nginx
	Using default tag: latest
	Trying to pull repository docker.io/library/nginx ... 
	latest: Pulling from docker.io/library/nginx
	fc7181108d40: Already exists 
	d2e987ca2267: Pull complete 
	0b760b431b11: Pull complete 
	Digest: sha256:96fb261b66270b900ea5a2c17a26abbfabe95506e73c3a3c65869a6dbe83223a
	Status: Downloaded newer image for docker.io/nginx:latest


#### 跑个NG例子

	[root@master mac]# kubectl run nginx-deployment --image=nginx --replicas=2
	kubectl run --generator=deployment/apps.v1 is DEPRECATED and will be removed in a future version. Use kubectl run --generator=run-pod/v1 or kubectl create instead.
	deployment.apps/nginx-deployment created
	[root@master mac]# 

#### 查看部署

	[root@master mac]# kubectl get deployment nginx-deployment
	NAME               READY   UP-TO-DATE   AVAILABLE   AGE
	nginx-deployment   0/2     2            0           30s
	[root@master mac]# 
	[root@master mac]# kubectl get pods
	NAME                                   READY   STATUS              RESTARTS   AGE
	nginx-deployment-55457b9d87-cj6v8      0/1     ContainerCreating   0          36s
	nginx-deployment-55457b9d87-ws6bd      0/1     ContainerCreating   0          36s
	[root@master mac]# 


#### 查看详细的部署
	
	[root@master mac]# kubectl describe deployment nginx-deployment
	Name:                   nginx-deployment
	Namespace:              default
	CreationTimestamp:      Wed, 03 Jul 2019 20:58:49 +0800
	Labels:                 run=nginx-deployment
	Annotations:            deployment.kubernetes.io/revision: 1
	Selector:               run=nginx-deployment
	Replicas:               2 desired | 2 updated | 2 total | 2 available | 0 unavailable
	StrategyType:           RollingUpdate
	MinReadySeconds:        0
	RollingUpdateStrategy:  25% max unavailable, 25% max surge
	Pod Template:
	  Labels:  run=nginx-deployment
	  Containers:
	   nginx-deployment:
	    Image:        nginx
	    Port:         <none>
	    Host Port:    <none>
	    Environment:  <none>
	    Mounts:       <none>
	  Volumes:        <none>
	Conditions:
	  Type           Status  Reason
	  ----           ------  ------
	  Available      True    MinimumReplicasAvailable
	  Progressing    True    NewReplicaSetAvailable
	OldReplicaSets:  <none>
	NewReplicaSet:   nginx-deployment-55457b9d87 (2/2 replicas created)
	Events:
	  Type    Reason             Age    From                   Message
	  ----    ------             ----   ----                   -------
	  Normal  ScalingReplicaSet  2m28s  deployment-controller  Scaled up replica set nginx-deployment-55457b9d87 to 2
	[root@master mac]# 

#### 查看复制

	[root@master mac]# kubectl get replicaset
	NAME                             DESIRED   CURRENT   READY   AGE
	nginx-deployment-55457b9d87      2         2         2       4m55s
	[root@master mac]# 

#### 查看详细的复制

	[root@master mac]# kubectl describe replicaset nginx-deployment-55457b9d87
	Name:           nginx-deployment-55457b9d87
	Namespace:      default
	Selector:       pod-template-hash=55457b9d87,run=nginx-deployment
	Labels:         pod-template-hash=55457b9d87
	                run=nginx-deployment
	Annotations:    deployment.kubernetes.io/desired-replicas: 2
	                deployment.kubernetes.io/max-replicas: 3
	                deployment.kubernetes.io/revision: 1
	Controlled By:  Deployment/nginx-deployment
	Replicas:       2 current / 2 desired
	Pods Status:    2 Running / 0 Waiting / 0 Succeeded / 0 Failed
	Pod Template:
	  Labels:  pod-template-hash=55457b9d87
	           run=nginx-deployment
	  Containers:
	   nginx-deployment:
	    Image:        nginx
	    Port:         <none>
	    Host Port:    <none>
	    Environment:  <none>
	    Mounts:       <none>
	  Volumes:        <none>
	Events:
	  Type    Reason            Age   From                   Message
	  ----    ------            ----  ----                   -------
	  Normal  SuccessfulCreate  20m   replicaset-controller  Created pod: nginx-deployment-55457b9d87-ws6bd
	  Normal  SuccessfulCreate  20m   replicaset-controller  Created pod: nginx-deployment-55457b9d87-cj6v8
	[root@master mac]# 


	[root@master mac]# kubectl get pods -o wide
	nginx-deployment-55457b9d87-cj6v8      1/1     Running   0          21m    10.38.0.3   node1.k8s   <none>           <none>
	nginx-deployment-55457b9d87-ws6bd      1/1     Running   0          21m    10.32.0.4   node2.k8s   <none>           <none>

#### 查看详细的Pod

	[root@master mac]# kubectl describe pod nginx-deployment-55457b9d87-cj6v8
	Name:           nginx-deployment-55457b9d87-cj6v8
	Namespace:      default
	Priority:       0
	Node:           node1.k8s/192.168.0.107
	Start Time:     Wed, 03 Jul 2019 20:58:49 +0800
	Labels:         pod-template-hash=55457b9d87
	                run=nginx-deployment
	Annotations:    <none>
	Status:         Running
	IP:             10.38.0.3
	Controlled By:  ReplicaSet/nginx-deployment-55457b9d87
	Containers:
	  nginx-deployment:
	    Container ID:   docker://4989daa8af25a74cbac5aaf85508e872d89d62522d6e4d7858333e7a0325d578
	    Image:          nginx
	    Image ID:       docker-pullable://docker.io/nginx@sha256:96fb261b66270b900ea5a2c17a26abbfabe95506e73c3a3c65869a6dbe83223a
	    Port:           <none>
	    Host Port:      <none>
	    State:          Running
	      Started:      Wed, 03 Jul 2019 21:00:59 +0800
	    Ready:          True
	    Restart Count:  0
	    Environment:    <none>
	    Mounts:
	      /var/run/secrets/kubernetes.io/serviceaccount from default-token-k6wtx (ro)
	Conditions:
	  Type              Status
	  Initialized       True 
	  Ready             True 
	  ContainersReady   True 
	  PodScheduled      True 
	Volumes:
	  default-token-k6wtx:
	    Type:        Secret (a volume populated by a Secret)
	    SecretName:  default-token-k6wtx
	    Optional:    false
	QoS Class:       BestEffort
	Node-Selectors:  <none>
	Tolerations:     node.kubernetes.io/not-ready:NoExecute for 300s
	                 node.kubernetes.io/unreachable:NoExecute for 300s
	Events:
	  Type     Reason     Age                From                Message
	  ----     ------     ----               ----                -------
	  Normal   Scheduled  22m                default-scheduler   Successfully assigned default/nginx-deployment-55457b9d87-cj6v8 to node1.k8s
	  Warning  Failed     21m                kubelet, node1.k8s  Failed to pull image "nginx": rpc error: code = Unknown desc = context canceled
	  Warning  Failed     21m                kubelet, node1.k8s  Error: ErrImagePull
	  Normal   BackOff    21m                kubelet, node1.k8s  Back-off pulling image "nginx"
	  Warning  Failed     21m                kubelet, node1.k8s  Error: ImagePullBackOff
	  Normal   Pulling    20m (x2 over 22m)  kubelet, node1.k8s  Pulling image "nginx"
	  Normal   Pulled     20m                kubelet, node1.k8s  Successfully pulled image "nginx"
	  Normal   Created    20m                kubelet, node1.k8s  Created container nginx-deployment
	  Normal   Started    20m                kubelet, node1.k8s  Started container nginx-deployment
	[root@master mac]# 

#### 总结一下

Deployment --> Replicaset  --> Pod

#### 删除资源

	[root@master mac]# kubectl delete all --all
	pod "httpd-app-5bc589d9f7-hds8g" deleted
	pod "httpd-app-5bc589d9f7-v45nw" deleted
	pod "kubernetes-bootcamp-7dc9765bf6-hvh6k" deleted
	pod "kubernetes-bootcamp-7dc9765bf6-pnh6s" deleted
	pod "nginx-deployment-55457b9d87-cj6v8" deleted
	pod "nginx-deployment-55457b9d87-ws6bd" deleted
	service "kubernetes" deleted
	service "kubernetes-bootcamp" deleted
	deployment.apps "httpd-app" deleted
	deployment.apps "kubernetes-bootcamp" deleted
	deployment.apps "nginx-deployment" deleted
	replicaset.apps "httpd-app-5bc589d9f7" deleted
	replicaset.apps "kubernetes-bootcamp-7dc9765bf6" deleted
	replicaset.apps "kubernetes-bootcamp-cfc74666" deleted
	replicaset.apps "nginx-deployment-55457b9d87" deleted
	[root@master mac]# 

#### 查看各种状态

	[root@master mac]# kubectl get deployments
	No resources found.
	[root@master mac]# 
	[root@master mac]# kubectl get services
	NAME         TYPE        CLUSTER-IP   EXTERNAL-IP   PORT(S)   AGE
	kubernetes   ClusterIP   10.96.0.1    <none>        443/TCP   107s
	[root@master mac]# 
	[root@master mac]# kubectl get pods
	No resources found.
	[root@master mac]# 


#### 命令 vs 配置文件

编辑nignx.yml

	[root@master demo_k8s]# cat nginx.yml 
	apiVersion: extensions/v1beta1
	kind: Deployment
	metadata:
	  name: nginx-manual
	spec:
	  replicas: 2
	  template: 
	    metadata:
	      labels:
	        app: web_server
	    spec:
	      containers:
	      - name: nginx
	        image: busybox


	[root@master demo_k8s]# ls -l
	total 4
	-rw-r--r--. 1 root root 236 Jul  4 11:00 nginx.yml
	[root@master demo_k8s]# 


查看K8S的Nodes信息：

	[root@master demo_k8s]# kubectl get nodes
	NAME         STATUS   ROLES    AGE     VERSION
	master.k8s   Ready    master   4d17h   v1.15.0
	node1.k8s    Ready    <none>   4d17h   v1.15.0
	node2.k8s    Ready    <none>   4d17h   v1.15.0
	[root@master demo_k8s]# 


查看K8S的Pods/Deployments信息：
	[root@master demo_k8s]# 
	[root@master demo_k8s]# kubectl get pods
	No resources found.
	[root@master demo_k8s]# 
	[root@master demo_k8s]# kubectl get deployments
	No resources found.
	[root@master demo_k8s]# 

使用配置文件创建部署：
	[root@master demo_k8s]# kubectl apply -f nginx.yml 
	deployment.extensions/nginx-manual created
	[root@master demo_k8s]# 
	[root@master demo_k8s]# kubectl get deployments
	NAME           READY   UP-TO-DATE   AVAILABLE   AGE
	nginx-manual   2/2     2            2           13s
	[root@master demo_k8s]# 

查看Pods的信息：

	[root@master demo_k8s]# kubectl get pods
	NAME                            READY   STATUS    RESTARTS   AGE
	nginx-manual-5c5d477cfd-8xs4w   1/1     Running   0          43s
	nginx-manual-5c5d477cfd-gtghc   1/1     Running   0          43s
	[root@master demo_k8s]# 

	[root@master demo_k8s]# kubectl get pods -o wide
	NAME                            READY   STATUS    RESTARTS   AGE   IP          NODE        NOMINATED NODE   READINESS GATES
	nginx-manual-5c5d477cfd-8xs4w   1/1     Running   0          59s   10.38.0.1   node1.k8s   <none>           <none>
	nginx-manual-5c5d477cfd-gtghc   1/1     Running   0          59s   10.32.0.2   node2.k8s   <none>           <none>
	[root@master demo_k8s]# 

测试手工部署的NG：

	[root@master demo_k8s]# curl 10.32.0.2
	<!DOCTYPE html>
	<html>
	<head>
	<title>Welcome to nginx!</title>
	<style>
	    body {
	        width: 35em;
	        margin: 0 auto;
	        font-family: Tahoma, Verdana, Arial, sans-serif;
	    }
	</style>
	</head>
	<body>
	<h1>Welcome to nginx!</h1>
	<p>If you see this page, the nginx web server is successfully installed and
	working. Further configuration is required.</p>
	
	<p>For online documentation and support please refer to
	<a href="http://nginx.org/">nginx.org</a>.<br/>
	Commercial support is available at
	<a href="http://nginx.com/">nginx.com</a>.</p>
	
	<p><em>Thank you for using nginx.</em></p>
	</body>
	</html>

删掉这些资源：

可以执行： kubectl delete deployment nginx-manual or kubectl delete -f nginx.yml:

	[root@master demo_k8s]# kubectl get pods
	NAME                            READY   STATUS             RESTARTS   AGE
	nginx-manual-779f5f6685-9xfqc   0/1     Completed          7          12m
	nginx-manual-779f5f6685-q69wn   0/1     CrashLoopBackOff   7          12m
	[root@master demo_k8s]# 
	[root@master demo_k8s]# kubectl get deployments
	NAME           READY   UP-TO-DATE   AVAILABLE   AGE
	nginx-manual   0/2     2            0           12m
	[root@master demo_k8s]# 
	[root@master demo_k8s]# kubectl delete deployment nginx-manual
	deployment.extensions "nginx-manual" deleted
	[root@master demo_k8s]# 

	[root@master demo_k8s]# kubectl delete -f nginx.yml 
	deployment.extensions "nginx-manual" deleted

	[root@master demo_k8s]# kubectl get deployments
	No resources found.
	[root@master demo_k8s]# 
	[root@master demo_k8s]# kubectl get pods
	No resources found.
	[root@master demo_k8s]# 

测试一下伸缩：

	[root@master demo_k8s]# cat nginx.yml 
	apiVersion: extensions/v1beta1
	kind: Deployment
	metadata:
	  name: nginx-manual
	spec:
	  replicas: 5
	  template: 
	    metadata:
	      labels:
	        app: web_server
	    spec:
	      containers:
	      - name: nginx
	        image: nginx:latest
	
	[root@master demo_k8s]# 
	[root@master demo_k8s]# kubectl apply -f nginx.yml 
	deployment.extensions/nginx-manual created
	[root@master demo_k8s]# 
	[root@master demo_k8s]# kubectl get pods -o wide
	NAME                            READY   STATUS    RESTARTS   AGE   IP          NODE        NOMINATED NODE   READINESS GATES
	nginx-manual-5c5d477cfd-4rcdv   1/1     Running   0          39s   10.38.0.3   node1.k8s   <none>           <none>
	nginx-manual-5c5d477cfd-ck7q9   1/1     Running   0          39s   10.38.0.2   node1.k8s   <none>           <none>
	nginx-manual-5c5d477cfd-d9nqq   1/1     Running   0          39s   10.32.0.2   node2.k8s   <none>           <none>
	nginx-manual-5c5d477cfd-zh7sx   1/1     Running   0          39s   10.32.0.3   node2.k8s   <none>           <none>
	nginx-manual-5c5d477cfd-zlcxd   1/1     Running   0          39s   10.38.0.1   node1.k8s   <none>           <none>
	[root@master demo_k8s]# 

五个副本被创建并调度到node1和node2.
由于出于安全的考虑，默认情况下，K8S不会将Pod调度到Master节点。 如果希望将K8S Master也当作Node使用，可以执行如下命令：

	[root@master demo_k8s]# kubectl taint node master.k8s node-role.kubenetes.io/master-
	[root@master demo_k8s]# kubectl taint node master.k8s node-role.kubenetes.io/master="":NoSchedule


减少副本数为3个：

	[root@master demo_k8s]# cat nginx.yml 
	apiVersion: extensions/v1beta1
	kind: Deployment
	metadata:
	  name: nginx-manual
	spec:
	  replicas: 3
	  template: 
	    metadata:
	      labels:
	        app: web_server
	    spec:
	      containers:
	      - name: nginx
	        image: nginx:latest
	
	[root@master demo_k8s]# 
	[root@master demo_k8s]# kubectl get pods
	NAME                            READY   STATUS    RESTARTS   AGE
	nginx-manual-5c5d477cfd-4rcdv   1/1     Running   0          5m6s
	nginx-manual-5c5d477cfd-ck7q9   1/1     Running   0          5m6s
	nginx-manual-5c5d477cfd-d9nqq   1/1     Running   0          5m6s
	nginx-manual-5c5d477cfd-zh7sx   1/1     Running   0          5m6s
	nginx-manual-5c5d477cfd-zlcxd   1/1     Running   0          5m6s
	[root@master demo_k8s]# 

	[root@master demo_k8s]# kubectl apply -f nginx.yml 
	deployment.extensions/nginx-manual configured
	[root@master demo_k8s]# 

	[root@master demo_k8s]# kubectl get pods
	NAME                            READY   STATUS        RESTARTS   AGE
	nginx-manual-5c5d477cfd-4rcdv   0/1     Terminating   0          5m43s
	nginx-manual-5c5d477cfd-ck7q9   1/1     Running       0          5m43s
	nginx-manual-5c5d477cfd-zh7sx   1/1     Running       0          5m43s
	nginx-manual-5c5d477cfd-zlcxd   1/1     Running       0          5m43s
	[root@master demo_k8s]# 

	[root@master demo_k8s]# kubectl get pods
	NAME                            READY   STATUS    RESTARTS   AGE
	nginx-manual-5c5d477cfd-ck7q9   1/1     Running   0          5m48s
	nginx-manual-5c5d477cfd-zh7sx   1/1     Running   0          5m48s
	nginx-manual-5c5d477cfd-zlcxd   1/1     Running   0          5m48s
	[root@master demo_k8s]# 

	[root@master demo_k8s]# kubectl get pods -o wide
	NAME                            READY   STATUS    RESTARTS   AGE     IP          NODE        NOMINATED NODE   READINESS GATES
	nginx-manual-5c5d477cfd-ck7q9   1/1     Running   0          6m50s   10.38.0.2   node1.k8s   <none>           <none>
	nginx-manual-5c5d477cfd-zh7sx   1/1     Running   0          6m50s   10.32.0.3   node2.k8s   <none>           <none>
	nginx-manual-5c5d477cfd-zlcxd   1/1     Running   0          6m50s   10.38.0.1   node1.k8s   <none>           <none>
	[root@master demo_k8s]# 

模拟Failover

	[mac@node2 ~]$ 
	[mac@node2 ~]$ sudo halt -h
	[sudo] password for mac: 

检查Pods情况：

	[root@master demo_k8s]# kubectl get pods -o wide
	NAME                            READY   STATUS        RESTARTS   AGE     IP          NODE        NOMINATED NODE   READINESS GATES
	nginx-manual-5c5d477cfd-ck7q9   1/1     Running       0          15m     10.38.0.2   node1.k8s   <none>           <none>
	nginx-manual-5c5d477cfd-k7287   1/1     Running       0          2m15s   10.38.0.3   node1.k8s   <none>           <none>
	nginx-manual-5c5d477cfd-zh7sx   1/1     Terminating   0          15m     10.32.0.3   node2.k8s   <none>           <none>
	nginx-manual-5c5d477cfd-zlcxd   1/1     Running       0          15m     10.38.0.1   node1.k8s   <none>           <none>
	[root@master demo_k8s]# 

用Label控制Pod的位置

	[root@master demo_k8s]# kubectl get nodes
	NAME         STATUS   ROLES    AGE     VERSION
	master.k8s   Ready    master   4d18h   v1.15.0
	node1.k8s    Ready    <none>   4d17h   v1.15.0
	node2.k8s    Ready    <none>   4d17h   v1.15.0
	[root@master demo_k8s]# 
	[root@master demo_k8s]# kubectl label node node1.k8s disktype=ssd
	node/node1.k8s labeled
	[root@master demo_k8s]# kubectl get nodes --show-labels
	NAME         STATUS   ROLES    AGE     VERSION   LABELS
	master.k8s   Ready    master   4d18h   v1.15.0   beta.kubernetes.io/arch=amd64,beta.kubernetes.io/os=linux,kubernetes.io/arch=amd64,kubernetes.io/hostname=master.k8s,kubernetes.io/os=linux,node-role.kubernetes.io/master=
	node1.k8s    Ready    <none>   4d18h   v1.15.0   beta.kubernetes.io/arch=amd64,beta.kubernetes.io/os=linux,kubernetes.io/arch=amd64,kubernetes.io/hostname=node1.k8s,kubernetes.io/os=linux,disktype=ssd
	node2.k8s    Ready    <none>   4d17h   v1.15.0   beta.kubernetes.io/arch=amd64,beta.kubernetes.io/os=linux,kubernetes.io/arch=amd64,kubernetes.io/hostname=node2.k8s,kubernetes.io/os=linux
	[root@master demo_k8s]# 

在Pod模板里通过nodeSelector指定此Pod的部署到具有label disktype=ssd的Node1上。

	[root@master demo_k8s]# kubectl get pods
	No resources found.
	[root@master demo_k8s]# 
	[root@master demo_k8s]# kubectl get deployments
	No resources found.
	[root@master demo_k8s]# 
	[root@master demo_k8s]# cat nginx-ssd.yml 
	apiVersion: extensions/v1beta1
	kind: Deployment
	metadata:
	  name: nginx-manual
	spec:
	  replicas: 3
	  template: 
	    metadata:
	      labels:
	        app: web_server
	    spec:
	      containers:
	      - name: nginx
	        image: nginx:latest
	      nodeSelector:
	        disktype: ssd
	[root@master demo_k8s]# kubectl apply -f nginx-ssd.yml 
	deployment.extensions/nginx-manual created
	[root@master demo_k8s]# 
	[root@master demo_k8s]# kubectl get pods
	NAME                            READY   STATUS              RESTARTS   AGE
	nginx-manual-687868fcbd-8h667   0/1     ContainerCreating   0          7s
	nginx-manual-687868fcbd-lrlfw   0/1     ContainerCreating   0          7s
	nginx-manual-687868fcbd-r2mpq   0/1     ContainerCreating   0          7s
	[root@master demo_k8s]# 
	[root@master demo_k8s]# kubectl get pods -o wide
	NAME                            READY   STATUS              RESTARTS   AGE   IP          NODE        NOMINATED NODE   READINESS GATES
	nginx-manual-687868fcbd-8h667   0/1     ContainerCreating   0          18s   <none>      node1.k8s   <none>           <none>
	nginx-manual-687868fcbd-lrlfw   1/1     Running             0          18s   10.38.0.1   node1.k8s   <none>           <none>
	nginx-manual-687868fcbd-r2mpq   0/1     ContainerCreating   0          18s   <none>      node1.k8s   <none>           <none>
	[root@master demo_k8s]# 
	[root@master demo_k8s]# vi nginx-ssd.yml 
	apiVersion: extensions/v1beta1
	kind: Deployment
	metadata:
	  name: nginx-manual
	spec:
	  replicas: 6
	  template:
	    metadata:
	      labels:
	        app: web_server
	    spec:
	      containers:
	      - name: nginx
	        image: nginx:latest
	      nodeSelector:
	        disktype: ssd
	~
	
	"nginx-ssd.yml" 16L, 282C written
	[root@master demo_k8s]# 

	[root@master demo_k8s]# kubectl get pods -o wide
	NAME                            READY   STATUS    RESTARTS   AGE   IP          NODE        NOMINATED NODE   READINESS GATES
	nginx-manual-687868fcbd-8h667   1/1     Running   0          57s   10.38.0.3   node1.k8s   <none>           <none>
	nginx-manual-687868fcbd-lrlfw   1/1     Running   0          57s   10.38.0.1   node1.k8s   <none>           <none>
	nginx-manual-687868fcbd-r2mpq   1/1     Running   0          57s   10.38.0.2   node1.k8s   <none>           <none>

	[root@master demo_k8s]# kubectl apply -f nginx-ssd.yml 
	deployment.extensions/nginx-manual configured

	[root@master demo_k8s]# kubectl get pods
	NAME                            READY   STATUS              RESTARTS   AGE
	nginx-manual-687868fcbd-8h667   1/1     Running             0          70s
	nginx-manual-687868fcbd-lrlfw   1/1     Running             0          70s
	nginx-manual-687868fcbd-r2mpq   1/1     Running             0          70s
	nginx-manual-687868fcbd-2p8vz   0/1     ContainerCreating   0          5s
	nginx-manual-687868fcbd-4k4fl   0/1     ContainerCreating   0          5s
	nginx-manual-687868fcbd-bfbzj   0/1     ContainerCreating   0          5s

	[root@master demo_k8s]# kubectl get pods -o wide
	NAME                            READY   STATUS              RESTARTS   AGE   IP          NODE        NOMINATED NODE   READINESS GATES
	nginx-manual-687868fcbd-lrlfw   1/1     Running             0          74s   10.38.0.1   node1.k8s   <none>           <none>
	nginx-manual-687868fcbd-r2mpq   1/1     Running             0          74s   10.38.0.2   node1.k8s   <none>           <none>
	nginx-manual-687868fcbd-8h667   1/1     Running             0          74s   10.38.0.3   node1.k8s   <none>           <none>
	nginx-manual-687868fcbd-2p8vz   0/1     ContainerCreating   0          9s    <none>      node1.k8s   <none>           <none>
	nginx-manual-687868fcbd-4k4fl   0/1     ContainerCreating   0          9s    <none>      node1.k8s   <none>           <none>
	nginx-manual-687868fcbd-bfbzj   0/1     ContainerCreating   0          9s    <none>      node1.k8s   <none>           <none>
	[root@master demo_k8s]# 

删掉指定的Label disktype， 执行如下的命令：


	[root@master demo_k8s]# kubectl label node node1.k8s disktype-
	node/node1.k8s labeled
	[root@master demo_k8s]# 

	[root@master demo_k8s]# kubectl get nodes --show-labels
	NAME         STATUS   ROLES    AGE     VERSION   LABELS
	master.k8s   Ready    master   4d18h   v1.15.0   beta.kubernetes.io/arch=amd64,beta.kubernetes.io/os=linux,kubernetes.io/arch=amd64,kubernetes.io/hostname=master.k8s,kubernetes.io/os=linux,node-role.kubernetes.io/master=
	node1.k8s    Ready    <none>   4d18h   v1.15.0   beta.kubernetes.io/arch=amd64,beta.kubernetes.io/os=linux,kubernetes.io/arch=amd64,kubernetes.io/hostname=node1.k8s,kubernetes.io/os=linux
	node2.k8s    Ready    <none>   4d18h   v1.15.0   beta.kubernetes.io/arch=amd64,beta.kubernetes.io/os=linux,kubernetes.io/arch=amd64,kubernetes.io/hostname=node2.k8s,kubernetes.io/os=linux
	[root@master demo_k8s]# 

删掉了label，此时Pod并不会重新部署，依旧会在K8S的Node1上运行。

	[root@master demo_k8s]# kubectl get pods -o wide
	NAME                            READY   STATUS    RESTARTS   AGE     IP          NODE        NOMINATED NODE   READINESS GATES
	nginx-manual-687868fcbd-2p8vz   1/1     Running   0          6m48s   10.38.0.4   node1.k8s   <none>           <none>
	nginx-manual-687868fcbd-4k4fl   1/1     Running   0          6m48s   10.38.0.6   node1.k8s   <none>           <none>
	nginx-manual-687868fcbd-8h667   1/1     Running   0          7m53s   10.38.0.3   node1.k8s   <none>           <none>
	nginx-manual-687868fcbd-bfbzj   1/1     Running   0          6m48s   10.38.0.5   node1.k8s   <none>           <none>
	nginx-manual-687868fcbd-lrlfw   1/1     Running   0          7m53s   10.38.0.1   node1.k8s   <none>           <none>
	nginx-manual-687868fcbd-r2mpq   1/1     Running   0          7m53s   10.38.0.2   node1.k8s   <none>           <none>
	[root@master demo_k8s]# 
	[root@master demo_k8s]# kubectl get pods
	NAME                            READY   STATUS    RESTARTS   AGE
	nginx-manual-687868fcbd-2p8vz   1/1     Running   0          6m53s
	nginx-manual-687868fcbd-4k4fl   1/1     Running   0          6m53s
	nginx-manual-687868fcbd-8h667   1/1     Running   0          7m58s
	nginx-manual-687868fcbd-bfbzj   1/1     Running   0          6m53s
	nginx-manual-687868fcbd-lrlfw   1/1     Running   0          7m58s
	nginx-manual-687868fcbd-r2mpq   1/1     Running   0          7m58s
	[root@master demo_k8s]# 

除非在nginx.yml 中删掉 nodeSelector的设置， 然后通过 kubectl apply 来重新部署。

	[root@master demo_k8s]# kubectl get pods -o wide
	NAME                            READY   STATUS    RESTARTS   AGE   IP          NODE        NOMINATED NODE   READINESS GATES
	nginx-manual-687868fcbd-2p8vz   1/1     Running   0          10m   10.38.0.4   node1.k8s   <none>           <none>
	nginx-manual-687868fcbd-4k4fl   1/1     Running   0          10m   10.38.0.6   node1.k8s   <none>           <none>
	nginx-manual-687868fcbd-8h667   1/1     Running   0          11m   10.38.0.3   node1.k8s   <none>           <none>
	nginx-manual-687868fcbd-bfbzj   1/1     Running   0          10m   10.38.0.5   node1.k8s   <none>           <none>
	nginx-manual-687868fcbd-lrlfw   1/1     Running   0          11m   10.38.0.1   node1.k8s   <none>           <none>
	nginx-manual-687868fcbd-r2mpq   1/1     Running   0          11m   10.38.0.2   node1.k8s   <none>           <none>
	[root@master demo_k8s]# 
	[root@master demo_k8s]# kubectl apply -f nginx-ssd.yml 
	deployment.extensions/nginx-manual configured
	[root@master demo_k8s]# 

K8S会删除之前的Pods，并且调度和运行新的Pods，这些Pods分布在两个节点上。

	[root@master demo_k8s]# kubectl get pods -o wide
	NAME                            READY   STATUS    RESTARTS   AGE   IP          NODE        NOMINATED NODE   READINESS GATES
	nginx-manual-5c5d477cfd-2nj57   1/1     Running   0          30s   10.38.0.6   node1.k8s   <none>           <none>
	nginx-manual-5c5d477cfd-g8fsc   1/1     Running   0          11s   10.32.0.4   node2.k8s   <none>           <none>
	nginx-manual-5c5d477cfd-khcvx   1/1     Running   0          11s   10.38.0.2   node1.k8s   <none>           <none>
	nginx-manual-5c5d477cfd-lfglr   1/1     Running   0          18s   10.32.0.3   node2.k8s   <none>           <none>
	nginx-manual-5c5d477cfd-rlftk   1/1     Running   0          18s   10.38.0.4   node1.k8s   <none>           <none>
	nginx-manual-5c5d477cfd-wjjvr   1/1     Running   0          30s   10.32.0.2   node2.k8s   <none>           <none>
	[root@master demo_k8s]# 

### DaementSet

与replicaset类似，区别在于，每个node最多只能运行一个副本。

	[root@master mac]# kubectl get replicaset
	NAME                      DESIRED   CURRENT   READY   AGE
	nginx-manual-5c5d477cfd   6         6         6       44m
	nginx-manual-687868fcbd   0         0         0       56m
	[root@master mac]# 

DaemonSet的典型应用场景：


	[root@master mac]# kubectl get daemonset
	No resources found.

K8S自己就在用DaemonSet运行系统组件，需要查看 kube-system 命名空间

	[root@master mac]# kubectl get daemonset --namespace=kube-system
	NAME         DESIRED   CURRENT   READY   UP-TO-DATE   AVAILABLE   NODE SELECTOR                 AGE
	kube-proxy   3         3         3       3            3           beta.kubernetes.io/os=linux   4d19h
	weave-net    3         3         3       3            3           <none>                        3d19h
	[root@master mac]# 

weave-net 和 kube-proxy 需要系统组件，不指定命名空间，返回默认命名空间 （Default）中的资源。

由于无法拿到kube-proxy的YAML文件，只能运行如下的命令来查看配置：

	[root@master mac]# kubectl edit daemonset kube-proxy --namespace=kube-system

运行自己的DaemonSet

Prometheus 流行的系统监控方案, Node exporter 是 Prometheus的agent，以DaemonSet的形式运行在每个被监控的节点上。

通过https://hub.docker.com/r/prom/node-exporter，获取Docker镜像．

	# Prometheus exporter for machine metrics, written in Go with pluggable metric collectors.
	docker pull prom/node-exporter

### Job

容器按照持续运行的时间可以分为： 服务类容器和工作类容器

- K8S的Deployment，ReplicaSet，DaemonSet都是用于管理服务类容器
- 工作类容器则是一次性的任务 （比如： 跑批处理）

先看一下简单的Job配置文件

	[root@master demo_k8s]# cat myjob.yml 
	apiVersion: batch/v1
	kind: Job
	metadata:
	  name: myjob
	spec:
	  template: 
	    metadata:
	      name: myjob
	    spec:
	      containers:
	      - name: hello
	        image: busybox
	        command: ['echo' , 'hello k8s job!']
	      restartPolicy: Never
	
	[root@master demo_k8s]# 
	
通过kubectl apply 来启动job：

	[root@master demo_k8s]# kubectl apply -f myjob.yml 
	job.batch/myjob created
	[root@master demo_k8s]# 
	
查看Job：

	[root@master demo_k8s]# kubectl get job
	NAME    COMPLETIONS   DURATION   AGE
	myjob   1/1           23s        4m35s
	[root@master demo_k8s]# 

	[root@master demo_k8s]# kubectl get pod 
	NAME                            READY   STATUS      RESTARTS   AGE
	myjob-wkv2h                     0/1     Completed   0          45s
	nginx-manual-5c5d477cfd-2nj57   1/1     Running     0          144m
	nginx-manual-5c5d477cfd-g8fsc   1/1     Running     0          143m
	nginx-manual-5c5d477cfd-khcvx   1/1     Running     0          143m
	nginx-manual-5c5d477cfd-lfglr   1/1     Running     0          144m
	nginx-manual-5c5d477cfd-rlftk   1/1     Running     0          144m
	nginx-manual-5c5d477cfd-wjjvr   1/1     Running     0          144m
	[root@master demo_k8s]# 
	
通过kubectl logs 可以查看Pod的标准输出：

	[root@master demo_k8s]# kubectl logs myjob-wkv2h
	hello k8s job!
	[root@master demo_k8s]# 

Pod失败的情况：

做个实验，修改myjob.yml, 故意引人一个错误，如下文字：

	[root@master demo_k8s]# cat myjob.yml 
	apiVersion: batch/v1
	kind: Job
	metadata:
	  name: myjob
	spec:
	  template: 
	    metadata:
	      name: myjob
	    spec:
	      containers:
	      - name: hello
	        image: busybox
	        command: ['invalid_command' , 'hello k8s job!']
	      restartPolicy: Never

先删除之前的Job：

	[root@master demo_k8s]# kubectl delete -f myjob.yml 
	job.batch "myjob" deleted
	[root@master demo_k8s]# 

	[root@master demo_k8s]# kubectl get jobs
	No resources found.

运行新的job，并且查看状态：

	[root@master demo_k8s]# kubectl apply -f myjob.yml
	job.batch/myjob created
	[root@master demo_k8s]# 

	[root@master demo_k8s]# kubectl get job
	NAME    COMPLETIONS   DURATION   AGE
	myjob   0/1           11s        11s
	[root@master demo_k8s]# 

可以看到有多个Pod，状态均不正常.

	[root@master demo_k8s]# kubectl get pods
	NAME                            READY   STATUS               RESTARTS   AGE
	myjob-22vrn                     0/1     ContainerCannotRun   0          31s
	myjob-mwxqc                     0/1     ContainerCannotRun   0          51s
	myjob-t2wpv                     0/1     ContainerCreating    0          1s
	nginx-manual-5c5d477cfd-2nj57   1/1     Running              0          154m
	nginx-manual-5c5d477cfd-g8fsc   1/1     Running              0          153m
	nginx-manual-5c5d477cfd-khcvx   1/1     Running              0          153m
	nginx-manual-5c5d477cfd-lfglr   1/1     Running              0          153m
	nginx-manual-5c5d477cfd-rlftk   1/1     Running              0          153m
	nginx-manual-5c5d477cfd-wjjvr   1/1     Running              0          154m
	[root@master demo_k8s]# 

通过kubectl describe pod 查看某个pod的启动日志：

	[root@master demo_k8s]# kubectl describe pod myjob-22vrn
	Name:           myjob-22vrn
	Namespace:      default
	Priority:       0
	Node:           node2.k8s/192.168.0.108
	Start Time:     Thu, 04 Jul 2019 14:30:29 +0800
	Labels:         controller-uid=d5fdd738-cb5a-4a09-b59f-7636a9e04496
	                job-name=myjob
	Annotations:    <none>
	Status:         Failed
	IP:             10.32.0.5
	Controlled By:  Job/myjob
	Containers:
	  hello:
	    Container ID:  docker://636322c965f6767ba3619f15c07d803705166d2802ff977136bfece37bbfb37a
	    Image:         busybox
	    Image ID:      docker-pullable://docker.io/busybox@sha256:c94cf1b87ccb80f2e6414ef913c748b105060debda482058d2b8d0fce39f11b9
	    Port:          <none>
	    Host Port:     <none>
	    Command:
	      invalid_command
	      hello k8s job!
	    State:      Terminated
	      Reason:   ContainerCannotRun
	      Message:  oci runtime error: container_linux.go:235: starting container process caused "exec: \"invalid_command\": executable file not found in $PATH"
	
	      Exit Code:    127
	      Started:      Thu, 04 Jul 2019 14:30:38 +0800
	      Finished:     Thu, 04 Jul 2019 14:30:38 +0800
	    Ready:          False
	    Restart Count:  0
	    Environment:    <none>
	    Mounts:
	      /var/run/secrets/kubernetes.io/serviceaccount from default-token-k6wtx (ro)
	Conditions:
	  Type              Status
	  Initialized       True 
	  Ready             False 
	  ContainersReady   False 
	  PodScheduled      True 
	Volumes:
	  default-token-k6wtx:
	    Type:        Secret (a volume populated by a Secret)
	    SecretName:  default-token-k6wtx
	    Optional:    false
	QoS Class:       BestEffort
	Node-Selectors:  <none>
	Tolerations:     node.kubernetes.io/not-ready:NoExecute for 300s
	                 node.kubernetes.io/unreachable:NoExecute for 300s
	Events:
	  Type     Reason     Age   From                Message
	  ----     ------     ----  ----                -------
	  Normal   Scheduled  51s   default-scheduler   Successfully assigned default/myjob-22vrn to node2.k8s
	  Normal   Pulling    49s   kubelet, node2.k8s  Pulling image "busybox"
	  Normal   Pulled     41s   kubelet, node2.k8s  Successfully pulled image "busybox"
	  Normal   Created    41s   kubelet, node2.k8s  Created container hello
	  Warning  Failed     41s   kubelet, node2.k8s  Error: failed to start container "hello": Error response from daemon: oci runtime error: container_linux.go:235: starting container process caused "exec: \"invalid_command\": executable file not found in $PATH"
	[root@master demo_k8s]# 

结论： 日志显示没有可以执行的程序。

	starting container process caused "exec: \"invalid_command\": executable file not found in $PATH"

试试 restartPolicy： OnFailure。

此时的效果应该是： 保持Pod的数量是1个，但是不断的在RESTARTS，**说明了OnFailure生效了，容器失败后会自动重启**。

	[root@master demo_k8s]# cat myjob.yml 
	apiVersion: batch/v1
	kind: Job
	metadata:
	  name: myjob
	spec:
	  template: 
	    metadata:
	      name: myjob
	    spec:
	      containers:
	      - name: hello
	        image: busybox
	        command: ['invalid_command' , 'hello k8s job!']
	      restartPolicy: OnFailure
	
	[root@master demo_k8s]# 
	[root@master demo_k8s]# kubectl apply -f myjob.yml 
	job.batch/myjob created
	[root@master demo_k8s]# 
	[root@master demo_k8s]# kubectl get pods
	NAME                            READY   STATUS              RESTARTS   AGE
	myjob-97797                     0/1     ContainerCreating   0          6s
	nginx-manual-5c5d477cfd-2nj57   1/1     Running             0          161m
	nginx-manual-5c5d477cfd-g8fsc   1/1     Running             0          161m
	nginx-manual-5c5d477cfd-khcvx   1/1     Running             0          161m
	nginx-manual-5c5d477cfd-lfglr   1/1     Running             0          161m
	nginx-manual-5c5d477cfd-rlftk   1/1     Running             0          161m
	nginx-manual-5c5d477cfd-wjjvr   1/1     Running             0          161m
	[root@master demo_k8s]# 
	
	[root@master demo_k8s]# kubectl get pods
	NAME                            READY   STATUS              RESTARTS   AGE
	myjob-97797                     0/1     RunContainerError   3          80s
	nginx-manual-5c5d477cfd-2nj57   1/1     Running             0          163m
	nginx-manual-5c5d477cfd-g8fsc   1/1     Running             0          162m
	nginx-manual-5c5d477cfd-khcvx   1/1     Running             0          162m
	nginx-manual-5c5d477cfd-lfglr   1/1     Running             0          162m
	nginx-manual-5c5d477cfd-rlftk   1/1     Running             0          162m
	nginx-manual-5c5d477cfd-wjjvr   1/1     Running             0          163m
	[root@master demo_k8s]# 

Job的并行性

有时候我们希望能够同时运行多个Pod，提供job的执行效率，可以通过 parallelism 设置。

	[root@master demo_k8s]# cat myjob_paralelism.yml 
	apiVersion: batch/v1
	kind: Job
	metadata:
	  name: myjob
	spec:
	  parallelism: 2
	  template: 
	    metadata:
	      name: myjob
	    spec:
	      containers:
	      - name: hello
	        image: busybox
	        command: ['echo' , 'hello k8s job!']
	      restartPolicy: Never
	
我们希望并行的Pod数量是2，通过kubectl apply实践一下：

	[root@master demo_k8s]# 
	[root@master demo_k8s]# kubectl apply -f myjob_paralelism.yml 
	job.batch/myjob created
	[root@master demo_k8s]# 

	[root@master demo_k8s]# kubectl get jobs
	NAME    COMPLETIONS   DURATION   AGE
	myjob   0/1 of 2      8s         8s
	[root@master demo_k8s]# 

	[root@master demo_k8s]# kubectl get pods
	NAME                            READY   STATUS      RESTARTS   AGE
	myjob-f6wgl                     0/1     Completed   0          16s
	myjob-s5tq2                     0/1     Completed   0          16s
	[root@master demo_k8s]# 

	[root@master demo_k8s]# kubectl get pods -o wide
	NAME                            READY   STATUS      RESTARTS   AGE    IP          NODE        NOMINATED NODE   READINESS GATES
	myjob-f6wgl                     0/1     Completed   0          27s    10.32.0.5   node2.k8s   <none>           <none>
	myjob-s5tq2                     0/1     Completed   0          27s    10.38.0.1   node1.k8s   <none>           <none>

	[root@master demo_k8s]# 
	[root@master demo_k8s]# kubectl logs myjob-s5tq2
	hello k8s job!
	[root@master demo_k8s]# kubectl logs myjob-f6wgl
	hello k8s job!
	[root@master demo_k8s]# 

我们还可以通过completions设置Job成功完成对Pod的总数。

	[root@master demo_k8s]# cat myjob_paralelism_completions.yml 
	apiVersion: batch/v1
	kind: Job
	metadata:
	  name: myjob
	spec:
	  parallelism: 2
	  completions: 6
	  template: 
	    metadata:
	      name: myjob
	    spec:
	      containers:
	      - name: hello
	        image: busybox
	        command: ['echo' , 'hello k8s job!']
	      restartPolicy: Never
	
	[root@master demo_k8s]# kubectl get job
	No resources found.
	[root@master demo_k8s]# kubectl apply -f myjob_paralelism_completions.yml 
	job.batch/myjob created
	[root@master demo_k8s]# 

这样配置的意义： 每次运行两个Pod，直到总共6个Pod成功完成。
	
	[root@master demo_k8s]# kubectl get job
	NAME    COMPLETIONS   DURATION   AGE
	myjob   6/6           53s        59s
	[root@master demo_k8s]# 

	[root@master demo_k8s]# kubectl get pods -o wide
	NAME                            READY   STATUS      RESTARTS   AGE    IP          NODE        NOMINATED NODE   READINESS GATES
	myjob-4z6vg                     0/1     Completed   0          19s    10.32.0.5   node2.k8s   <none>           <none>
	myjob-5tqtf                     0/1     Completed   0          54s    10.38.0.1   node1.k8s   <none>           <none>
	myjob-7fhjj                     0/1     Completed   0          10s    10.38.0.1   node1.k8s   <none>           <none>
	myjob-k5mrw                     0/1     Completed   0          54s    10.32.0.5   node2.k8s   <none>           <none>
	myjob-ldhn8                     0/1     Completed   0          40s    10.32.0.5   node2.k8s   <none>           <none>
	myjob-zhtsd                     0/1     Completed   0          29s    10.32.0.5   node2.k8s   <none>           <none>
	[root@master demo_k8s]# 

清楚旧的Job资源：

	[root@master demo_k8s]# kubectl delete -f myjob_paralelism_completions.yml 
	job.batch "myjob" deleted
	[root@master demo_k8s]# 
	[root@master demo_k8s]# kubectl get jobs
	No resources found.
	[root@master demo_k8s]# 


定时Job：

	[root@master demo_k8s]# kubectl api-versions
	admissionregistration.k8s.io/v1beta1
	apiextensions.k8s.io/v1beta1
	apiregistration.k8s.io/v1
	apiregistration.k8s.io/v1beta1
	apps/v1
	apps/v1beta1
	apps/v1beta2
	authentication.k8s.io/v1
	authentication.k8s.io/v1beta1
	authorization.k8s.io/v1
	authorization.k8s.io/v1beta1
	autoscaling/v1
	autoscaling/v2beta1
	autoscaling/v2beta2
	batch/v1
	batch/v1beta1
	certificates.k8s.io/v1beta1
	coordination.k8s.io/v1
	coordination.k8s.io/v1beta1
	events.k8s.io/v1beta1
	extensions/v1beta1
	networking.k8s.io/v1
	networking.k8s.io/v1beta1
	node.k8s.io/v1beta1
	policy/v1beta1
	rbac.authorization.k8s.io/v1
	rbac.authorization.k8s.io/v1beta1
	scheduling.k8s.io/v1
	scheduling.k8s.io/v1beta1
	storage.k8s.io/v1
	storage.k8s.io/v1beta1
	v1
	[root@master demo_k8s]# 
	
定义定时任务：

	[root@master demo_k8s]# cat myjob_cron.yml 
	apiVersion: batch/v1beta1
	kind: CronJob
	metadata:
	  name: hello
	spec:
	  schedule: "0,15,30,45 * * * *"
	  jobTemplate:
	    spec:
	      template:
	        spec:
	          restartPolicy: OnFailure
	          containers:
	          - name: hello
	            image: busybox
	            command: ['echo' , 'hello k8s job!']
	[root@master demo_k8s]# 
	
创建CronJob：

	[root@master demo_k8s]# kubectl apply -f myjob_cron.yml 
	cronjob.batch/hello created
	[root@master demo_k8s]# 
	
查看CronJob：
	
	[root@master demo_k8s]# kubectl get cronjob
	NAME    SCHEDULE             SUSPEND   ACTIVE   LAST SCHEDULE   AGE
	hello   0,15,30,45 * * * *   False     0        <none>          117s
	[root@master demo_k8s]# 
	[root@master demo_k8s]# kubectl get cronjob -o wide
	NAME    SCHEDULE             SUSPEND   ACTIVE   LAST SCHEDULE   AGE     CONTAINERS   IMAGES    SELECTOR
	hello   0,15,30,45 * * * *   False     0        <none>          2m31s   hello        busybox   <none>
	[root@master demo_k8s]# 

但是定时执行，并没有成功，需要继续研究。。。。

	[root@master demo_k8s]# kubectl delete all --all
	pod "nginx-manual-5c5d477cfd-2nj57" deleted
	pod "nginx-manual-5c5d477cfd-g8fsc" deleted
	pod "nginx-manual-5c5d477cfd-khcvx" deleted
	pod "nginx-manual-5c5d477cfd-lfglr" deleted
	pod "nginx-manual-5c5d477cfd-rlftk" deleted
	pod "nginx-manual-5c5d477cfd-wjjvr" deleted
	service "kubernetes" deleted
	deployment.apps "nginx-manual" deleted
	replicaset.apps "nginx-manual-5c5d477cfd" deleted
	replicaset.apps "nginx-manual-687868fcbd" deleted
	[root@master demo_k8s]# 

## 10 通过Service来访问Pod

### 创建服务

先来创建一个部署：

	[root@master demo_k8s]# cat httpd.yml 
	apiVersion: apps/v1beta1
	kind: Deployment
	metadata:
	  name: httpd
	spec:
	  replicas: 3
	  template: 
	    metadata:
	      labels:
	        app: httpd
	    spec:
	      containers:
	      - name: httpd
	        image: httpd:latest
	        ports:
	        - containerPort: 80
	[root@master demo_k8s]# 
	[root@master demo_k8s]# kubectl apply -f httpd.yml 
	deployment.apps/httpd created
	[root@master demo_k8s]# 
	[root@master demo_k8s]# kubectl get pod -o wide
	NAME                     READY   STATUS              RESTARTS   AGE   IP       NODE        NOMINATED NODE   READINESS GATES
	httpd-784bc79c6c-2ltj4   0/1     ContainerCreating   0          15s   <none>   node2.k8s   <none>           <none>
	httpd-784bc79c6c-4kgz6   0/1     ContainerCreating   0          15s   <none>   node1.k8s   <none>           <none>
	httpd-784bc79c6c-9m4tg   0/1     ContainerCreating   0          15s   <none>   node2.k8s   <none>           <none>
	>   

接下来，我创建一个服务

	[root@master demo_k8s]# cat httpd-svc.yml 
	apiVersion: v1
	kind: Service
	metadata:
	  name: httpd-svc
	spec:
	  selector:
	    app: httpd
	  ports:
	  - protocol: TCP
	    port: 8080
	    targetPort: 80
	
	[root@master demo_k8s]# 
	
	[root@master demo_k8s]# kubectl apply -f httpd-svc.yml 
	service/httpd-svc created
	[root@master demo_k8s]# 

查看服务：

	[root@master demo_k8s]# kubectl get services
	NAME         TYPE        CLUSTER-IP      EXTERNAL-IP   PORT(S)    AGE
	httpd-svc    ClusterIP   10.105.43.114   <none>        8080/TCP   3s
	kubernetes   ClusterIP   10.96.0.1       <none>        443/TCP    85m
	[root@master demo_k8s]# 

httpd-svc 分配一个CLUSTER-IP 10.105.43.114, 可以通过此IP访问后的的 httpd Pod

测试服务：

	[root@master demo_k8s]# curl 10.105.43.114:8080
	<html><body><h1>It works!</h1></body></html>
	[root@master demo_k8s]# 

查看详细的服务信息：

[root@master demo_k8s]# kubectl describe service httpd-svc
Name:              httpd-svc
Namespace:         default
Labels:            <none>
Annotations:       kubectl.kubernetes.io/last-applied-configuration:
                     {"apiVersion":"v1","kind":"Service","metadata":{"annotations":{},"name":"httpd-svc","namespace":"default"},"spec":{"ports":[{"port":8080,"...
Selector:          app=httpd
Type:              ClusterIP
IP:                10.105.43.114
Port:              <unset>  8080/TCP
TargetPort:        80/TCP
Endpoints:         10.32.0.2:80,10.32.0.3:80,10.38.0.1:80
Session Affinity:  None
Events:            <none>
[root@master demo_k8s]# 

Endpoints罗列了三个Pod的IP和端口：

	Endpoints:         10.32.0.2:80,10.32.0.3:80,10.38.0.1:80

	[root@master mac]# kubectl get endpoints
	NAME                  ENDPOINTS                                      AGE
	kubernetes            192.168.0.106:6443                             3h16m
	kubernetes-bootcamp   10.32.0.2:8080,10.38.0.1:8080,10.38.0.2:8080   3h11m
	[root@master mac]# 


问题：

- Service的Cluster IP在哪里配置？
- Cluster IP又是如何映射到Port IP？

答案： iptables



### Cluster IP底层实现

ClusterIP是一个虚拟IP，是由K8S节点上的iptables规则管理的，可以是iptables-save打印输出。

	[root@master demo_k8s]# iptables-save | grep httpd
	-A KUBE-SERVICES -d 10.105.43.114/32 -p tcp -m comment --comment "default/httpd-svc: cluster IP" -m tcp --dport 8080 -j KUBE-SVC-RL3JAE4GN7VOGDGP

	[root@master demo_k8s]# iptables-save | grep  KUBE
	...
	-A KUBE-SEP-4HB24K6IP2IWWEH3 -s 10.38.0.1/32 -j KUBE-MARK-MASQ
	-A KUBE-SEP-4HB24K6IP2IWWEH3 -p tcp -m tcp -j DNAT --to-destination 10.38.0.1:80
	...
	-A KUBE-SEP-B727ZMBVOQCVSQ5D -s 10.32.0.3/32 -j KUBE-MARK-MASQ
	-A KUBE-SEP-B727ZMBVOQCVSQ5D -p tcp -m tcp -j DNAT --to-destination 10.32.0.3:80
	...
	-A KUBE-SEP-GVYF3X5TWDRIEMT6 -s 10.32.0.2/32 -j KUBE-MARK-MASQ
	-A KUBE-SEP-GVYF3X5TWDRIEMT6 -p tcp -m tcp -j DNAT --to-destination 10.32.0.2:80
	...

解释一下，下面的规则：

	-A KUBE-SERVICES -d 10.105.43.114/32 -p tcp -m comment --comment "default/httpd-svc: cluster IP" -m tcp --dport 8080 -j KUBE-SVC-RL3JAE4GN7VOGDGP
	-A KUBE-SVC-RL3JAE4GN7VOGDGP -m statistic --mode random --probability 0.33332999982 -j KUBE-SEP-GVYF3X5TWDRIEMT6
	-A KUBE-SVC-RL3JAE4GN7VOGDGP -m statistic --mode random --probability 0.50000000000 -j KUBE-SEP-B727ZMBVOQCVSQ5D
	-A KUBE-SVC-RL3JAE4GN7VOGDGP -j KUBE-SEP-4HB24K6IP2IWWEH3

即将请求分别转发到后端的三个Pod，通过上面的分析，我们可以得出结论：iptables将访问Service的流量转发到后端的Pod，而且使用类似**轮询的负载均衡策略**。

### DNS 访问服务

kubeadm 部署时会默认安装一个kube-dns的组件：

	[root@master mac]# kubectl get deployment --namespace=kube-system
	NAME      READY   UP-TO-DATE   AVAILABLE   AGE
	coredns   2/2     2            2           5d1h
	[root@master mac]# 
	
kube-dns (coredns) 是一个DNS服务器。 有新服务被创建，kube-dns会添加该service的DNS记录.

使用下面的方式创建一个临时的busybox Pod，来验证DNS的有效性。

	[root@master mac]# 
	[root@master mac]# kubectl run busybox --rm -it --image=busybox /bin/sh
	kubectl run --generator=deployment/apps.v1 is DEPRECATED and will be removed in a future version. Use kubectl run --generator=run-pod/v1 or kubectl create instead.
	dIf you don't see a command prompt, try pressing enter.
	/ # ls
	bin   dev   etc   home  proc  root  run   sys   tmp   usr   var
	/ # 
	/ # wget httpd-svc:8080
	Connecting to httpd-svc:8080 (10.105.43.114:8080)
	saving to 'index.html'
	index.html           100% |********************************************************************************************************************|    45  0:00:00 ETA
	'index.html' saved
	
	/ # wget httpd-svc.default:8080
	Connecting to httpd-svc.default:8080 (10.105.43.114:8080)
	wget: can't open 'index.html': File exists

Cluster 中 Pod 可以通过： <SERVICE_NAME>.<NAMESAPCE_NAME> 来访问该服务。

	wget httpd-svc.default:8080
	wget httpd-svc:8080

或者使用nslookup

	/ # nslookup httpd-svc
	Server:         10.96.0.10
	Address:        10.96.0.10:53
	
	Name:   httpd-svc.default.svc.cluster.local
	Address: 10.105.43.114
	
	*** Can't find httpd-svc.svc.cluster.local: No answer
	*** Can't find httpd-svc.cluster.local: No answer
	*** Can't find httpd-svc.k8s: No answer
	*** Can't find httpd-svc.default.svc.cluster.local: No answer
	*** Can't find httpd-svc.svc.cluster.local: No answer
	*** Can't find httpd-svc.cluster.local: No answer
	*** Can't find httpd-svc.k8s: No answer
	/ # 

完整域名：
	
	httpd-svc.default.svc.cluster.local 是httpd-svc的完整域名。

如果要访问其他namespace中的服务，就必须带上namespace了。

查看Pod中的env：

	[root@master mac]# kubectl run busybox --rm -it --image=busybox /bin/sh
	kubectl run --generator=deployment/apps.v1 is DEPRECATED and will be removed in a future version. Use kubectl run --generator=run-pod/v1 or kubectl create instead.
	If you don't see a command prompt, try pressing enter.
	/ # 
	/ # ls
	bin   dev   etc   home  proc  root  run   sys   tmp   usr   var
	/ # env
	KUBERNETES_PORT=tcp://10.96.0.1:443
	KUBERNETES_SERVICE_PORT=443
	HOSTNAME=busybox-7cbc9ff64b-c8cgg
	SHLVL=1
	HOME=/root
	TERM=xterm
	KUBERNETES_PORT_443_TCP_ADDR=10.96.0.1
	PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin
	KUBERNETES_PORT_443_TCP_PORT=443
	KUBERNETES_BOOTCAMP_PORT_8080_TCP_ADDR=10.111.22.127
	KUBERNETES_PORT_443_TCP_PROTO=tcp
	KUBERNETES_BOOTCAMP_SERVICE_HOST=10.111.22.127
	KUBERNETES_BOOTCAMP_PORT_8080_TCP_PORT=8080
	KUBERNETES_BOOTCAMP_PORT_8080_TCP_PROTO=tcp
	KUBERNETES_BOOTCAMP_SERVICE_PORT=8080
	KUBERNETES_BOOTCAMP_PORT=tcp://10.111.22.127:8080
	KUBERNETES_PORT_443_TCP=tcp://10.96.0.1:443
	KUBERNETES_SERVICE_PORT_HTTPS=443
	KUBERNETES_SERVICE_HOST=10.96.0.1
	PWD=/
	KUBERNETES_BOOTCAMP_PORT_8080_TCP=tcp://10.111.22.127:8080
	/ # 


查看K8S所有的命名空间：

	[root@master mac]# kubectl get namespace
	NAME              STATUS   AGE
	default           Active   5d1h
	kube-node-lease   Active   5d1h
	kube-public       Active   5d1h
	kube-system       Active   5d1h
	[root@master mac]# 

### 外网如何访问服务

K8S提供了多种类型的Service，默认是：ClusterIP

- Cluster IP
- Node Port
- LoadBalancer

测试 Node Port：

	[root@master demo_k8s]# cat httpd-svc.yml 
	apiVersion: v1
	kind: Service
	metadata:
	  name: httpd-svc
	spec:
	  type: NodePort
	  selector:
	    app: httpd
	  ports:
	  - protocol: TCP
	    port: 8080
	    targetPort: 80
	
	[root@master demo_k8s]# 
	[root@master demo_k8s]# kubectl get svc
	NAME         TYPE        CLUSTER-IP      EXTERNAL-IP   PORT(S)    AGE
	httpd-svc    ClusterIP   10.105.43.114   <none>        8080/TCP   131m
	kubernetes   ClusterIP   10.96.0.1       <none>        443/TCP    3h36m
	[root@master demo_k8s]# 
	[root@master demo_k8s]# kubectl apply -f httpd-svc.yml 
	service/httpd-svc configured
	[root@master demo_k8s]# 
	[root@master demo_k8s]# kubectl get svc
	NAME         TYPE        CLUSTER-IP      EXTERNAL-IP   PORT(S)          AGE
	httpd-svc    NodePort    10.105.43.114   <none>        8080:30680/TCP   131m
	kubernetes   ClusterIP   10.96.0.1       <none>        443/TCP          3h37m
	[root@master demo_k8s]# 

通过30680的IP必须是Node IP，不能是虚拟IP；通过8080的IP是虚拟IP。

	[root@master demo_k8s]# curl master.k8s:8080
	curl: (7) Failed connect to master.k8s:8080; Connection refused
	[root@master demo_k8s]# curl master.k8s:30680
	<html><body><h1>It works!</h1></body></html>
	
	[root@master demo_k8s]# curl 10.105.43.114:8080
	<html><body><h1>It works!</h1></body></html>
	[root@master demo_k8s]# curl 10.105.43.114:30680
	^C
	
通过三个节点的IP+30680都可以访问http-svc

	[root@master demo_k8s]# curl 192.168.0.106:30680
	<html><body><h1>It works!</h1></body></html>
	[root@master demo_k8s]# curl 192.168.0.107:30680
	<html><body><h1>It works!</h1></body></html>
	[root@master demo_k8s]# curl 192.168.0.108:30680
	<html><body><h1>It works!</h1></body></html>
	[root@master demo_k8s]# 

深入探讨： K8S是如何将 NodeIP：NodePort 映射到Pod呢？

与ClusterIP一样，也是借助于iptables. 与ClusterIP相比，每个Node的iptables中都增加了

	[root@master demo_k8s]# iptables-save | grep http
	-A KUBE-NODEPORTS -p tcp -m comment --comment "default/httpd-svc:" -m tcp --dport 30680 -j KUBE-MARK-MASQ
	-A KUBE-NODEPORTS -p tcp -m comment --comment "default/httpd-svc:" -m tcp --dport 30680 -j KUBE-SVC-RL3JAE4GN7VOGDGP
	-A KUBE-SERVICES -d 10.96.0.1/32 -p tcp -m comment --comment "default/kubernetes:https cluster IP" -m tcp --dport 443 -j KUBE-SVC-NPX46M4PTMTKRN6Y
	-A KUBE-SERVICES -d 10.105.43.114/32 -p tcp -m comment --comment "default/httpd-svc: cluster IP" -m tcp --dport 8080 -j KUBE-SVC-RL3JAE4GN7VOGDGP
	[root@master demo_k8s]#

node1 iptables：

	[mac@node1 ~]$ sudo iptables-save | grep http
	[sudo] password for mac: 
	-A KUBE-NODEPORTS -p tcp -m comment --comment "default/httpd-svc:" -m tcp --dport 30680 -j KUBE-MARK-MASQ
	-A KUBE-NODEPORTS -p tcp -m comment --comment "default/httpd-svc:" -m tcp --dport 30680 -j KUBE-SVC-RL3JAE4GN7VOGDGP
	-A KUBE-SERVICES -d 10.96.0.1/32 -p tcp -m comment --comment "default/kubernetes:https cluster IP" -m tcp --dport 443 -j KUBE-SVC-NPX46M4PTMTKRN6Y
	-A KUBE-SERVICES -d 10.105.43.114/32 -p tcp -m comment --comment "default/httpd-svc: cluster IP" -m tcp --dport 8080 -j KUBE-SVC-RL3JAE4GN7VOGDGP
	[mac@node1 ~]$ 

nodePort是默认随机选择的，不过我们可以用NodePort指定某个特定端口。

	[root@master demo_k8s]# cat httpd-svc.yml 
	apiVersion: v1
	kind: Service
	metadata:
	  name: httpd-svc
	spec:
	  type: NodePort
	  selector:
	    app: httpd
	  ports:
	  - protocol: TCP
	    nodePort: 30000
	    port: 8080
	    targetPort: 80

现在配置文件中有了三个Port：

- nodePort: 节点上监听的端口。
- port: ClusterIP上监听的端口。
- targetPort: Pod监听的端口。

最终， Node和Cluster IP在各自的端口上接收到请求都会通过iptables转发到Pod的targetPort。

	[root@master demo_k8s]# cat httpd-svc.yml
	apiVersion: v1
	kind: Service
	metadata:
	  name: httpd-svc
	spec:
	  type: NodePort
	  selector:
	    app: httpd
	  ports:
	  - protocol: TCP
	    nodePort: 30000
	    port: 8080
	    targetPort: 80
	
	[root@master demo_k8s]# kubectl apply -f httpd-svc.yml 
	service/httpd-svc configured
	[root@master demo_k8s]# 

	[root@master demo_k8s]# kubectl get  services httpd-svc
	NAME        TYPE       CLUSTER-IP      EXTERNAL-IP   PORT(S)          AGE
	httpd-svc   NodePort   10.105.43.114   <none>        8080:30000/TCP   149m
	[root@master demo_k8s]# 

	[root@master demo_k8s]# curl 192.168.0.106:30000
	<html><body><h1>It works!</h1></body></html>
	[root@master demo_k8s]# curl 192.168.0.107:30000
	<html><body><h1>It works!</h1></body></html>
	[root@master demo_k8s]# curl 192.168.0.108:30000
	<html><body><h1>It works!</h1></body></html>
	[root@master demo_k8s]# 

好了，今天的玩转K8S到此结束，清楚资源：

	[root@master demo_k8s]# kubectl delete all --all
	pod "httpd-784bc79c6c-2ltj4" deleted
	pod "httpd-784bc79c6c-4kgz6" deleted
	pod "httpd-784bc79c6c-9m4tg" deleted
	service "httpd-svc" deleted
	service "kubernetes" deleted
	deployment.apps "httpd" deleted
	replicaset.apps "httpd-784bc79c6c" deleted
	[root@master demo_k8s]# 

## 11 滚动更新 Rolling Update

### 实践

使用版本1：jocatalin/kubernetes-bootcamp:v1

	[root@master demo_k8s]# cat bootcamp.yml 
	apiVersion: apps/v1beta1
	kind: Deployment
	metadata:
	  name: bootcamp
	spec:
	  replicas: 3
	  template: 
	    metadata:
	      labels:
	        app: bootcamp
	    spec:
	      containers:
	      - name: bootcamp
	        image: jocatalin/kubernetes-bootcamp:v1
	        ports:
	        - containerPort: 80
	[root@master demo_k8s]# 

	[root@master demo_k8s]# kubectl apply -f bootcamp.yml 
	deployment.apps/bootcamp created
	[root@master demo_k8s]# 

创建部署： bootcamp

	[root@master demo_k8s]# kubectl get deployment -o wide
	NAME       READY   UP-TO-DATE   AVAILABLE   AGE   CONTAINERS   IMAGES                             SELECTOR
	bootcamp   3/3     3            3           22s   bootcamp     jocatalin/kubernetes-bootcamp:v1   app=bootcamp
	[root@master demo_k8s]# 

创建复制： bootcamp-5fccdf47f7

	[root@master demo_k8s]# kubectl get replicaset -o wide
	NAME                  DESIRED   CURRENT   READY   AGE   CONTAINERS   IMAGES                             SELECTOR
	bootcamp-5fccdf47f7   3         3         3       37s   bootcamp     jocatalin/kubernetes-bootcamp:v1   app=bootcamp,pod-template-hash=5fccdf47f7
	[root@master demo_k8s]# 

创建三个Pod： bootcamp-5fccdf47f7-****

	[root@master demo_k8s]# kubectl get pod -o wide
	NAME                        READY   STATUS    RESTARTS   AGE   IP          NODE        NOMINATED NODE   READINESS GATES
	bootcamp-5fccdf47f7-c54wx   1/1     Running   0          53s   10.38.0.1   node1.k8s   <none>           <none>
	bootcamp-5fccdf47f7-v59xf   1/1     Running   0          53s   10.32.0.2   node2.k8s   <none>           <none>
	bootcamp-5fccdf47f7-zvtl8   1/1     Running   0          53s   10.38.0.2   node1.k8s   <none>           <none>
	[root@master demo_k8s]# 

暴露服务

	[root@master demo_k8s]# kubectl expose deployment/bootcamp --type="NodePort" --port 8080
	service/bootcamp exposed
	[root@master demo_k8s]# 
	[root@master demo_k8s]# kubectl get svc
	NAME         TYPE        CLUSTER-IP    EXTERNAL-IP   PORT(S)          AGE
	bootcamp     NodePort    10.96.82.20   <none>        8080:30695/TCP   7s
	[root@master demo_k8s]# 

测试服务：

	[root@master demo_k8s]# curl master.k8s:30695
	Hello Kubernetes bootcamp! | Running on: bootcamp-5fccdf47f7-v59xf | v=1
	[root@master demo_k8s]# 

升级镜像为V2版本，再次执行kubectl apply:

	[root@master demo_k8s]# cat bootcamp.yml 
	apiVersion: apps/v1beta1
	kind: Deployment
	metadata:
	  name: bootcamp
	spec:
	  replicas: 3
	  template: 
	    metadata:
	      labels:
	        app: bootcamp
	    spec:
	      containers:
	      - name: bootcamp
	        image: jocatalin/kubernetes-bootcamp:v2
	        ports:
	        - containerPort: 80
	[root@master demo_k8s]# 

	[root@master demo_k8s]# kubectl apply -f bootcamp.yml 
	deployment.apps/bootcamp configured
	[root@master demo_k8s]# 

将镜像升级后，看到：jocatalin/kubernetes-bootcamp:v2  
	[root@master demo_k8s]# kubectl get deployment -o wide
	NAME       READY   UP-TO-DATE   AVAILABLE   AGE     CONTAINERS   IMAGES                             SELECTOR
	bootcamp   3/3     3            3           9m52s   bootcamp     jocatalin/kubernetes-bootcamp:v2   app=bootcamp
	[root@master demo_k8s]# 

将镜像升级后，看到新旧的复制共存：

	[root@master demo_k8s]# kubectl get replicaset -o wide
	NAME                  DESIRED   CURRENT   READY   AGE   CONTAINERS   IMAGES                             SELECTOR
	bootcamp-5fccdf47f7   0         0         0       10m   bootcamp     jocatalin/kubernetes-bootcamp:v1   app=bootcamp,pod-template-hash=5fccdf47f7
	bootcamp-799b8b5d64   3         3         3       26s   bootcamp     jocatalin/kubernetes-bootcamp:v2   app=bootcamp,pod-template-hash=799b8b5d64
	[root@master demo_k8s]# 

将镜像升级后，看到新旧的Pods变化过程：

	[root@master demo_k8s]# 
	[root@master demo_k8s]# kubectl get pod -o wide
	NAME                        READY   STATUS        RESTARTS   AGE   IP          NODE        NOMINATED NODE   READINESS GATES
	bootcamp-5fccdf47f7-c54wx   0/1     Terminating   0          10m   10.38.0.1   node1.k8s   <none>           <none>
	bootcamp-5fccdf47f7-zvtl8   0/1     Terminating   0          10m   <none>      node1.k8s   <none>           <none>
	bootcamp-799b8b5d64-62pxd   1/1     Running       0          42s   10.38.0.3   node1.k8s   <none>           <none>
	bootcamp-799b8b5d64-zlgg4   1/1     Running       0          40s   10.32.0.4   node2.k8s   <none>           <none>
	bootcamp-799b8b5d64-zx762   1/1     Running       0          44s   10.32.0.3   node2.k8s   <none>           <none>

最终被三个新Pods 替代了：

	[root@master demo_k8s]# kubectl get pod 
	NAME                        READY   STATUS    RESTARTS   AGE
	bootcamp-799b8b5d64-62pxd   1/1     Running   0          58s
	bootcamp-799b8b5d64-zlgg4   1/1     Running   0          56s
	bootcamp-799b8b5d64-zx762   1/1     Running   0          60s
	[root@master demo_k8s]# 

使用NodePort 测试服务：

	[root@master demo_k8s]# kubectl get services
	NAME         TYPE        CLUSTER-IP    EXTERNAL-IP   PORT(S)          AGE
	bootcamp     NodePort    10.96.82.20   <none>        8080:30695/TCP   4m41s
	[root@master demo_k8s]#

	[root@master demo_k8s]# curl master.k8s:30695
	Hello Kubernetes bootcamp! | Running on: bootcamp-799b8b5d64-zlgg4 | v=2
	[root@master demo_k8s]# curl node1.k8s:30695
	Hello Kubernetes bootcamp! | Running on: bootcamp-799b8b5d64-zlgg4 | v=2
	[root@master demo_k8s]# curl node2.k8s:30695
	Hello Kubernetes bootcamp! | Running on: bootcamp-799b8b5d64-62pxd | v=2
	[root@master demo_k8s]# 

查看部署的具体替换过程：

	[root@master demo_k8s]# kubectl describe deployment bootcamp
	Name:                   bootcamp
	Namespace:              default
	CreationTimestamp:      Thu, 04 Jul 2019 19:36:38 +0800
	Labels:                 app=bootcamp
	Annotations:            deployment.kubernetes.io/revision: 2
	                        kubectl.kubernetes.io/last-applied-configuration:
	                          {"apiVersion":"apps/v1beta1","kind":"Deployment","metadata":{"annotations":{},"name":"bootcamp","namespace":"default"},"spec":{"replicas":...
	Selector:               app=bootcamp
	Replicas:               3 desired | 3 updated | 3 total | 3 available | 0 unavailable
	StrategyType:           RollingUpdate
	MinReadySeconds:        0
	RollingUpdateStrategy:  25% max unavailable, 25% max surge
	Pod Template:
	  Labels:  app=bootcamp
	  Containers:
	   bootcamp:
	    Image:        jocatalin/kubernetes-bootcamp:v2
	    Port:         80/TCP
	    Host Port:    0/TCP
	    Environment:  <none>
	    Mounts:       <none>
	  Volumes:        <none>
	Conditions:
	  Type           Status  Reason
	  ----           ------  ------
	  Available      True    MinimumReplicasAvailable
	  Progressing    True    NewReplicaSetAvailable
	OldReplicaSets:  <none>
	NewReplicaSet:   bootcamp-799b8b5d64 (3/3 replicas created)
	Events:
	  Type    Reason             Age    From                   Message
	  ----    ------             ----   ----                   -------
	  Normal  ScalingReplicaSet  15m    deployment-controller  Scaled up replica set bootcamp-5fccdf47f7 to 3
	  Normal  ScalingReplicaSet  5m28s  deployment-controller  Scaled up replica set bootcamp-799b8b5d64 to 1
	  Normal  ScalingReplicaSet  5m26s  deployment-controller  Scaled down replica set bootcamp-5fccdf47f7 to 2
	  Normal  ScalingReplicaSet  5m26s  deployment-controller  Scaled up replica set bootcamp-799b8b5d64 to 2
	  Normal  ScalingReplicaSet  5m24s  deployment-controller  Scaled down replica set bootcamp-5fccdf47f7 to 1
	  Normal  ScalingReplicaSet  5m24s  deployment-controller  Scaled up replica set bootcamp-799b8b5d64 to 3
	  Normal  ScalingReplicaSet  5m23s  deployment-controller  Scaled down replica set bootcamp-5fccdf47f7 to 0
	[root@master demo_k8s]# 

每次只更新替换一个Pod，每次提供的Pod数量是可以定制的。

	K8S提供了两个参数来精细控制Pod替换的数量：
	－maxSurge
	- maxUnavailable

### 回滚

快捷的方式：

	[root@master demo_k8s]# kubectl rollout undo deployment/bootcamp
	deployment.extensions/bootcamp rolled back
	[root@master demo_k8s]# 
	[root@master demo_k8s]# kubectl get pods -o wide
	NAME                        READY   STATUS        RESTARTS   AGE   IP          NODE        NOMINATED NODE   READINESS GATES
	bootcamp-5fccdf47f7-jbzxh   1/1     Running       0          10s   10.38.0.1   node1.k8s   <none>           <none>
	bootcamp-5fccdf47f7-t4pnj   1/1     Running       0          9s    10.32.0.2   node2.k8s   <none>           <none>
	bootcamp-5fccdf47f7-v296r   1/1     Running       0          6s    10.38.0.2   node1.k8s   <none>           <none>
	bootcamp-799b8b5d64-62pxd   1/1     Terminating   0          56m   10.38.0.3   node1.k8s   <none>           <none>
	bootcamp-799b8b5d64-zlgg4   1/1     Terminating   0          56m   10.32.0.4   node2.k8s   <none>           <none>
	bootcamp-799b8b5d64-zx762   1/1     Terminating   0          56m   10.32.0.3   node2.k8s   <none>           <none>
	[root@master demo_k8s]# 
	[root@master demo_k8s]# curl 10.96.82.20:8080
	Hello Kubernetes bootcamp! | Running on: bootcamp-5fccdf47f7-jbzxh | v=1
	[root@master demo_k8s]# 


K8S每次更新应用时候，都会记录下当前的配置，保存为一个reversion（版次），这样就可以回滚到某个特定的版次了。

通过 revisionHistoryLimit 属性增加revision数量：

对应httpd镜像： 2.4.16

	apiVersion: apps/v1beta1
	kind: Deployment
	metadata:
	  name: httpd
	spec:
	  revisionHistoryLimit: 10
	  replicas: 3
	  template: 
	    metadata:
	      labels:
	        app: httpd
	    spec:
	      containers:
	      - name: httpd
	        image: httpd:2.4.16
	        ports:
	        - containerPort: 80

对应httpd镜像： 2.4.17

	apiVersion: apps/v1beta1
	kind: Deployment
	metadata:
	  name: httpd
	spec:
	  revisionHistoryLimit: 10
	  replicas: 3
	  template: 
	    metadata:
	      labels:
	        app: httpd
	    spec:
	      containers:
	      - name: httpd
	        image: httpd:2.4.17
	        ports:
	        - containerPort: 80

对应httpd镜像： 2.4.18

	apiVersion: apps/v1beta1
	kind: Deployment
	metadata:
	  name: httpd
	spec:
	  revisionHistoryLimit: 10
	  replicas: 3
	  template: 
	    metadata:
	      labels:
	        app: httpd
	    spec:
	      containers:
	      - name: httpd
	        image: httpd:2.4.18
	        ports:
	        - containerPort: 80
	        - 

通过hubectl apply部署并更新应用：

	[root@master demo_k8s]# kubectl apply -f httpd.v1.yml --record
	deployment.apps/httpd created
	[root@master demo_k8s]# 

	[root@master demo_k8s]# kubectl get deployment -o wide
	NAME    READY   UP-TO-DATE   AVAILABLE   AGE   CONTAINERS   IMAGES         SELECTOR
	httpd   0/3     3            0           20s   httpd        httpd:2.4.16   app=httpd
	[root@master demo_k8s]# 

	[root@master demo_k8s]# kubectl apply -f httpd.v2.yml --record
	deployment.apps/httpd configured
	[root@master demo_k8s]# 

	[root@master demo_k8s]# kubectl get deployment -o wide
	NAME    READY   UP-TO-DATE   AVAILABLE   AGE    CONTAINERS   IMAGES         SELECTOR
	httpd   3/3     1            3           119s   httpd        httpd:2.4.17   app=httpd
	[root@master demo_k8s]# 

	[root@master demo_k8s]# kubectl apply -f httpd.v3.yml --record
	deployment.apps/httpd configured
	[root@master demo_k8s]# 

	[root@master demo_k8s]# kubectl get deployment -o wide
	NAME    READY   UP-TO-DATE   AVAILABLE   AGE     CONTAINERS   IMAGES         SELECTOR
	httpd   3/3     1            3           2m14s   httpd        httpd:2.4.18   app=httpd
	[root@master demo_k8s]# 

	[root@master demo_k8s]# kubectl rollout history deployment httpd
	deployment.extensions/httpd 
	REVISION  CHANGE-CAUSE
	1         kubectl apply --filename=httpd.v1.yml --record=true
	2         kubectl apply --filename=httpd.v2.yml --record=true
	3         kubectl apply --filename=httpd.v3.yml --record=true
	
	[root@master demo_k8s]# 

使用 -to-revision=1， 回滚到指定的版本

	[root@master demo_k8s]# kubectl rollout undo deployment httpd --to-revision=1
	deployment.extensions/httpd rolled back
	[root@master demo_k8s]# 
	[root@master demo_k8s]# kubectl rollout history deployment httpd
	deployment.extensions/httpd 
	REVISION  CHANGE-CAUSE
	2         kubectl apply --filename=httpd.v2.yml --record=true
	3         kubectl apply --filename=httpd.v3.yml --record=true
	4         kubectl apply --filename=httpd.v1.yml --record=true
	
	[root@master demo_k8s]# 

我们一定要在执行kubectl apply时加上 --record 参数。

下面是kubectl rollout undo 范例：

	Examples:
	  # Rollback to the previous deployment
	  kubectl rollout undo deployment/abc
	  
	  # Rollback to daemonset revision 3
	  kubectl rollout undo daemonset/abc --to-revision=3
	  
	  # Rollback to the previous deployment with dry-run
	  kubectl rollout undo --dry-run=true deployment/abc
	
	Options:
	      --allow-missing-template-keys=true: If true, ignore any errors in templates when a field or map key is missing in the template. Only applies to golang and jsonpath output formats.
	      --dry-run=false: If true, only print the object that would be sent, without sending it.
	  -f, --filename=[]: Filename, directory, or URL to files identifying the resource to get from a server.
	  -k, --kustomize='': Process the kustomization directory. This flag can't be used together with -f or -R.
	  -o, --output='': Output format. One of: json|yaml|name|go-template|go-template-file|template|templatefile|jsonpath|jsonpath-file.
	  -R, --recursive=false: Process the directory used in -f, --filename recursively. Useful when you want to manage related manifests organized within the same directory.
	      --template='': Template string or path to template file to use when -o=go-template, -o=go-template-file. The template format is golang templates [http://golang.org/pkg/text/template/#pkg-overview].
	      --to-revision=0: The revision to rollback to. Default to 0 (last revision).
	
	Usage:
	  kubectl rollout undo (TYPE NAME | TYPE/NAME) [flags] [options]
	
	Use "kubectl options" for a list of global command-line options (applies to all commands).

## 12 健康检查 Health Check


## 13 数据管理


## 14 Secret & Configmap


## 15 Helm - K8S的包管理器


## 16 网络


## 17 K8S的Dashboard


## 18 K8S的集群监控


## 19 K8S的集群日志管理


## 20 其他练习

### 删除Pod检测变化


#### 步骤01， 检测endpoints

	[root@master mac]# kubectl get endpoints
	NAME                  ENDPOINTS                                      AGE
	kubernetes            192.168.0.106:6443                             3h16m
	kubernetes-bootcamp   10.32.0.2:8080,10.38.0.1:8080,10.38.0.2:8080   3h11m
	[root@master mac]# 

#### 步骤02， 检测Pod

	[root@node1 ~]# kubectl get pods -o wide
	NAME                                   READY   STATUS    RESTARTS   AGE    IP          NODE        NOMINATED NODE   READINESS GATES
	kubernetes-bootcamp-7dc9765bf6-5mlg9   1/1     Running   0          3h3m   10.32.0.2   node2.k8s   <none>           <none>
	kubernetes-bootcamp-7dc9765bf6-c7jpd   1/1     Running   0          3h3m   10.38.0.1   node1.k8s   <none>           <none>
	kubernetes-bootcamp-7dc9765bf6-z65bl   1/1     Running   1          148m   10.38.0.2   node1.k8s   <none>           <none>
	[root@node1 ~]# 

#### 步骤03， 强制删除某个Pod

	[root@node1 ~]# kubectl delete pod kubernetes-bootcamp-7dc9765bf6-z65bl
	pod "kubernetes-bootcamp-7dc9765bf6-z65bl" deleted
	[root@node1 ~]# 

#### 步骤04， 检测Pod

	[root@node2 mac]# kubectl get pods -o wide
	NAME                                   READY   STATUS        RESTARTS   AGE    IP          NODE        NOMINATED NODE   READINESS GATES
	kubernetes-bootcamp-7dc9765bf6-4mp99   1/1     Running       0          23s    10.34.0.1   node3.k8s   <none>           <none>
	kubernetes-bootcamp-7dc9765bf6-5mlg9   1/1     Running       0          3h3m   10.32.0.2   node2.k8s   <none>           <none>
	kubernetes-bootcamp-7dc9765bf6-c7jpd   1/1     Running       0          3h3m   10.38.0.1   node1.k8s   <none>           <none>
	kubernetes-bootcamp-7dc9765bf6-z65bl   1/1     Terminating   1          148m   10.38.0.2   node1.k8s   <none>           <none>
	[root@node2 mac]# 

#### 步骤05， 检测endpoints

	[root@master mac]# kubectl get endpoints -w
	NAME                  ENDPOINTS                                      AGE
	kubernetes            192.168.0.106:6443                             3h17m
	kubernetes-bootcamp   10.32.0.2:8080,10.38.0.1:8080,10.38.0.2:8080   3h12m
	kubernetes-bootcamp   10.32.0.2:8080,10.38.0.1:8080                  3h13m
	kubernetes-bootcamp   10.32.0.2:8080,10.34.0.1:8080,10.38.0.1:8080   3h13m
	



