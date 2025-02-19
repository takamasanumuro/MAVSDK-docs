# C++ QuickStart

This quickstart shows you how to build and run a simple MAVSDK C++ example application against a simulated vehicle, and observe the operation using the console and in a ground station.

> **Note** MAVSDK is essentially a C++ library (or rather multiple library files) that you can include and link in your C++ application.


## Install MAVSDK library

### Linux

**Ubuntu**

If you have an older version already installed remove that first:
```
sudo apt remove mavsdk
```

The prebuilt C++ library can be downloaded as a **.deb** from [releases](https://github.com/mavlink/MAVSDK/releases), e.g.:

```
wget https://github.com/mavlink/MAVSDK/releases/download/v1.4.16/libmavsdk-dev_1.4.16_ubuntu20.04_amd64.deb
sudo dpkg -i libmavsdk-dev_1.4.16_ubuntu20.04_amd64.deb
```

### macOS

Install [Homebrew](https://brew.sh/) and use it to install the library:
```
brew install mavsdk
```

### Windows

For Windows you can download the **mavsdk-windows-x64-release.zip** file from [MAVSDK releases](https://github.com/mavlink/MAVSDK/releases) containing the headers and library and extract it locally (see [information how to use a locally installed library](guide/toolchain.md#sdk_local_install)).

For more detailed instructions or other platforms check out the [installation notes](guide/installation.md).

## Setting up a Simulator {#simulator}

The easiest way to try out MAVSDK is to run one of the MAVSDK examples against a simulated version of the vehicle.

To set up and run the PX4 simulator, you need to either [set up the PX4 SITL developer environment](https://docs.px4.io/master/en/dev_setup/dev_env.html).

Or use a [pre-built docker container to run PX4 and the simulator](https://github.com/JonasVautherin/px4-gazebo-headless):
```
docker run --rm -it jonasvautherin/px4-gazebo-headless:1.11.0
```

## Install QGroundControl

You can use *QGroundControl* to connect the simulator and observe vehicle movement and behaviour while the examples are running.
*QGroundControl* will automatically connect to the PX4 simulation as soon as it is started.

See [QGroundControl > Download and Install](https://docs.qgroundcontrol.com/en/getting_started/download_and_install.html) for information about setting up *QGroundControl* on your platform.


## Build and Try Example {#build_examples}

The examples are stored as part of the projects source code.
Get them using *git* in a terminal:
```
git clone https://github.com/mavlink/MAVSDK.git --recursive
cd MAVSDK
```

The examples can be found in the examples directory:
```
cd examples
```

To build the takeoff and land example, you can do:

```sh
cd takeoff_and_land/
cmake -Bbuild -H.
cmake --build build -j4
```

## Running an Example {#running_the_examples}

First start PX4 in SITL (Simulation) and *QGroundControl* as described above.

Then run the example app (from the **example/takeoff_land/build** directory) as shown:
```sh
build/takeoff_and_land udp://:14540
```

The MAVSDK application should connect to PX4, and you will be able to observe the example running in the SDK terminal, SITL terminal, and/or *QGroundControl*.
The expected behaviour is shown here: [Example: Takeoff and Land](examples/takeoff_and_land.md).

> **Note** The first argument above is the connection string (`udp://:14540`).
  This is the standard PX4 UDP port for connecting to offboard APIs (also see [Connecting to Systems](guide/connections.md)).


## Next Steps

Once MAVSDK is installed we recommend you:
- Try the [other examples](examples/README.md)
- See how to [write your own application](guide/toolchain.md) in C++.
- Browse the [API reference](api_reference/README.md) to get an overview of the functionality.
