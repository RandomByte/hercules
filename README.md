# [Hercules](https://github.com/RandomByte/hercules) Home Automation on Kubernetes

🚧 Work in progress. Not really ready for anything yet

**All Docker images used in this project are built for the armhf architecture (Raspberry Pi et al.) only.**  
However, it should be fairly easy to set this up on other architectures, you just need to build the Docker images yourself.


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
1. In the file `prod-cluster.yaml`, replace all variables with the appropriate values
	- `<external ip>`: Enter the external IP address of one of your nodes (preferably the 'master'), that should be used by external services to communicate with the MQTT and other servers within your cluster

1. Apply the template and start the Hercules infrastructure on your Kubernetes cluster (this will internally call kubectl):
	```sh
	kontemplate apply prod-cluster.yaml
	```

## Modules
Modules that are either running within the Kubernetes cluster or on external devices such as sensors. Communication happens via MQTT.

### Cluster Services
- [RandomByte/mqtt-traffic](https://github.com/RandomByte/mqtt-traffic)
- [RandomByte/mqtt-online-check](https://github.com/RandomByte/mqtt-online-check)

### External Services
- [RandomByte/esp8266-mqtt-light-sensor](https://github.com/RandomByte/esp8266-mqtt-light-sensor)
- [RandomByte/mqtt-nodemotion](https://github.com/RandomByte/mqtt-nodemotion)
- [RandomByte/mqtt-wifi-scanner](https://github.com/RandomByte/mqtt-wifi-scanner)

## License
Released under the [MIT License](https://opensource.org/licenses/MIT).
