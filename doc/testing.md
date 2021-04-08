# Unity Simulation Local Testing Guide
The goal of this guide is to walk through the steps to test a Linux Unity build on a non Linux OS using a Docker container. Testing a simulation locally before submitting to Unity Simulation will help to surface any issues experienced during execution.

## Download Docker
Go to https://www.docker.com/ to sign up and install Docker Desktop.
Please reference the [getting started guide](https://docs.docker.com/get-started/) for general information about Docker.

Platform Specific Documentation:
- [Docker Desktop for Mac](https://docs.docker.com/docker-for-mac/)
- [Docker Desktop for Windows](https://docs.docker.com/docker-for-windows/)

Find the `Advanced` section in either of the platform specific guides for information on resource allocation for Docker. **NOTE:** You may need to increase the allocation memory or CPU if the Unity build you are trying to execute is sufficiently large.

## Testing Quickstart Materials Linux Build
This guide assumes that you are following the Quickstart Guide and have downloaded the [Quickstart Materials](quickstart.md#download-unity-simulation-quickstart-materials).


Open the Quickstart Materials directory and navigate to the `RollaballLinuxBuild` directory. This directory should contain a single zipped file name `rollaball_linux_build.zip`. Unzip this file into a directory called `rollaball_linux_build` and ensure that the directory structure resembles the following.
```
  |-RollaballLinuxBuild
  |  |-rollaball_linux_build
  |  |  |-rollaball_linux_build_Data
  |  |  |-rollaball_linux_build.x86_64
  |  |  |-UnityPlayer.so
  |  |-rollaball_linux_build.zip
```


After unzipping the `rollaball_linux_build.zip` file, open the terminal and change your current directory to that of the Quickstart Materials to confirm contents.
```
$ cd /PATH/TO/QUICKSTART/MATERIALS
```
MacOS
```bash
$ls
```
Win
```
>dir
```
```
Outputs:
AppParams		Dockerfile		USimCLI			RollaballLinuxBuild		RunDefinitions		RunExecutionData
```


Next let's build the image defined in the `Dockerfile` file. NOTE: This command must be run from the Quickstart materials directory.
```
$docker build -t test-container .
```

If the image has been successfully built you can confirm by running the following command.

MacOS
```bash
$docker images | grep "test-container"

Outputs:
test-container      latest              856f2c231b06        2 minutes ago       1.1GB
```
Win
```
>docker images | findstr test-container

Outputs:
test-container      latest              856f2c231b06        2 minutes ago       1.1GB
```

Now that the image is built let's start it up and attach to the running container.
```
$docker run -it test-container /bin/bash
```

Once working in the container the terminal prompt should change to resemble something like `root@ff69abdf956e:/#`.

Let's first check that the executable and _Data directory was copied over correctly by running

MacOS
```bash
$ls /tmp/
```

Win
```
>dir /tmp/
```
```
Expected Output:
UnityPlayer.so	linux_build.x86_64  linux_build_Data
```

Now let's execute the build by running the follow command:

```
xvfb-run --auto-servernum --server-args="-screen 0 640x480x24:32" /tmp/linux_build.x86_64
```
`xvfb` is a command that is used to run executables on machines with no display hardware and in this case, our container.



If everything went well you should see some output similar to the output below. It may take a few minutes for the process to finish.
```
Found path: /tmp/linux_build.x86_64
```


All the logging by the executing sim is stored in this file:
```
/root/.config/unity3d/Unity Technologies/Roll-a-ball/Player.log
```
If you navigate to the output folder `/root/.config/unity3d/Unity Technologies/Roll-a-ball`, in there you should find a folder that is named after a randomly generated GUID, for example: `b2711fed-2219-4f03-b7ba-c73855628dd5`. That GUID will change each time a sim is executed. To list all of the screen captures taken by the Unity Simulation SDK, run:
```
ls {THE-RANDOM-GUID}/Screencapture/
```
You should see many files named like `Camera0_0.jpg`.

## Copying Files from Running Container to Local
Let's copy the generated screen captures from the running container to our local file system so we can view them easier.

First we need to get the running container's container id. In the terminal window running the container the `ff69abdf956e` portion of the prompt `root@ff69abdf956e:/#` is the container id although you can also get the container id by running the `docker ps` command in a **different** terminal window.

```
$docker ps

OUTPUTS:

CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS               NAMES
ff69abdf956e        test-container      "/bin/bash"         2 minutes ago       Up 2 minutes                            clever_mestorf
```

To Copy an entire directory from a running container to our local file system:
```
docker cp ff69abdf956e:"/root/.config/unity3d/Unity Technologies/Roll-a-ball/{THE-RANDOM-GUID}/ScreenCapture/" /PATH/TO/SAVE/SCREEN_CAPTURES/
```

To copy a single file:

```
docker cp ff69abdf956e:/PATH/TO/FILE/FILENAME.txt FILENAME.txt
```

## Testing Your Own Linux Build

You can also test your own project's Linux builds by only making a few changes.

Use the Dockerfile below or copy the `Dockerfile` in the Quickstart Materials to the directory where your Linux build was saved and change the `COPY` lines at the bottom to point at your executable, _Data directory, and UnityPlayer.so file.
```
# What is the base image to pull
FROM python:3.7.2-stretch

# Update package lists
RUN apt-get update

# Install xvfb to execute the Unity build in the container
RUN apt-get install -y xvfb


# Copy the executable and _Data directory to /unity_player
RUN mkdir /unity_player
COPY [YOUR_BUILD].x86_64 /unity_player/linux_build.x86_64
COPY [YOUR_BUILD]_Data /unity_player/linux_build_Data

# for 2019.2+ version of the Unity Editor
COPY [YOUR_BUILD]/UnityPlayer.so /unity_player/UnityPlayer.so
```

[Optional] You may omit copying your build files using docker's [bind mounting feature](https://docs.docker.com/storage/bind-mounts/) when you execute the docker run command.

Example of bind mounting:
```bash
$ docker run -it --rm --mount type=bind,source=/path/to/build,target=/unity_player test-container bash
```

Example Dockerfile when using bind mounting:
```
# What is the base image to pull
FROM python:3.7.2-stretch

# Update package lists
RUN apt-get update

# Install xvfb to execute the Unity build in the container
RUN apt-get install -y xvfb
```

## Loading App Params

If you are loading your app-params using the `Application.dataPath + "/StreamingAssets/"` as mentioned in the [SDK Integration guide](integrate.md#integrating-app-params) they should load just as they do when pressing Play with your simulation scene loaded from within the Unity Editor.
