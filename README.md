# [Hercules](https://github.com/RandomByte/hercules) Home Automation on Kubernetes

🚧 Not really ready for anything yet

All Docker images used in this project are **armhf (Raspberry Pi et al.) only.**


## Prerequisites
1. Have a running Kubernetes cluster on one or more Raspberry Pis
	- *The Docker images used in this project currently only support the Pis armhf architecture*
	- I highly recommend [this guide](https://gist.github.com/alexellis/fdbc90de7691a1b9edb545c17da2d975) by [@alexellis](https://github.com/alexellis)
1. Install [kontemplate](https://github.com/tazjin/kontemplate)
	- *I needed some templating tool and went with this one*

## Usage
1. Copy the file `prod-cluster.yaml.example` to `prod-cluster.yaml`:  
	```sh
	cp prod-cluster.yaml.example prod-cluster.yaml
	```
1. In the file `prod-cluster.yaml`, replace all placeholders (marked with `<` and `>`) with the appropriate values
	- `<external ip>`: Enter the external IP address of one of your nodes (preferably the 'master'), that should be used by external services to communicate with the MQTT and other servers within your cluster

1. Apply the template and start the Hercules infrastructure on your Kubernetes cluster (this will internally call kubectl):
	```sh
	kontemplate apply prod-cluster.yaml
	```

## License
Released under the [MIT License](https://opensource.org/licenses/MIT).
