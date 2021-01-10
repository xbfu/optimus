Steps to bring up Kubernetes 1.7 on Ubuntu 14.04<br/>
(1) configure ubuntu/config-default.sh<br/>
(2) modify the version of flannel, etcd and kubernetes in file download-release.sh<br/>
(3) comment out "verify-prereqs" and "verify-kube-binaries" in both kube-up.sh and kube-down.sh<br/>
(4) modify ubuntu/util.sh, add "KUBE_ROOT=/home/net/kubernetes/" in the begining. add "source ~/kube/config-default.sh" in function provision-master(), function provision-node() and function provision-masterandnode() just before "source ~/kube/util.sh".<br/>
(5) modify ubuntu/deployAddons.sh, replace the original two lines in the begining with "KUBE_ROOT=/home/net/kubernetes/" and KUBECTL="kubectl" in the begining, and exchange the order of starting DNS and UI (i.e., starting Dashboard first)<br/>
(6) update heapster-controller.yaml and influxdb-grafana-controller.yaml with newer version of images. Besides, delete "--threshold=5" and "--estimator=exponential"in heapster.<br/>
(7) add "--feature-gates=Accelerators=true" to config kubelet with GPU support in KUBE_ROOT/cluster/ubuntu/util.sh.<br/>
