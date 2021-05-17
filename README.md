# Example IoT Device

## Getting Started

Git clone this project in your machine.

### Prerequisites

Build tested on Ubuntu Server. Pistache doesn't support Windows, but you can use something like [WSL](https://docs.microsoft.com/en-us/windows/wsl/install-win10) or a virtual machine with Linux.

You will need to have a C++ compiler. I used g++ that came preinstalled. Check using `g++ -v`

You will need to install the [Pistache](https://github.com/pistacheio/pistache) library.
On Ubuntu, you can install a pre-built binary as described [here](http://pistache.io/docs/#installing-pistache).

#### MQTT

For MQTT protocol support, you can use the Eclipse [Paho](https://www.eclipse.org/paho) client library. The [Paho C++ library](https://github.com/eclipse/paho.mqtt.cpp#unix-and-linux) can be installed from source (will require you to also build and install the Paho C library).

MQTT also requires a server (a message broker) to be running in order to have where to send the messages. For this, you can use Eclipse [Mosquitto](https://mosquitto.org/). On Ubuntu, it can be installed from a PPA:

```sh
sudo apt-add-repository ppa:mosquitto-dev/mosquitto-ppa
sudo apt update
sudo apt install mosquitto
```

### Building

#### Using Make

You can build the `microwave` executable by running `make`.

### Manually

A step by step series of examples that tell you how to get a development env running

You should open the terminal, navigate into the root folder of this repository, and run\
`g++ -std=c++17 microwave_example.cpp -o microwave -lpistache -lcrypto -lssl -lpthread -lpaho-mqttpp3 -lpaho-mqtt3a`

This will compile the project using g++, into an executable called `microwave` using the libraries `pistache`, `crypto`, `ssl`, `pthread`. You only really want pistache, but the last three are dependencies of the former.
Note that in this compilation process, the order of the libraries is important.

`paho-mqttpp3` is the Paho C++ client library, and `paho-mqtt3a` is the C library it depends on.

### Running

In a separate terminal, start the Mosquitto server:

```sh
mosquitto -v
```

The `-v` argument starts it in verbose mode, meaning it will print out all incoming and outgoing messages.

To start the server run\
`./microwave`

Your server should display the number of cores being used and no errors.

If Mosquitto is running in another terminal, you will see a message sent by the microwave.

To test, open up another terminal, and type\
`curl http://localhost:9080/ready`

Number 1 should display.

Now you have the server running.


## Built With

* [Pistache](https://github.com/pistacheio/pistache) - Web server

## License

This project is licensed under the Apache 2.0 Open Source Licence - see the [LICENSE](LICENSE) file for details
