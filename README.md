# Unity Simulation Documentation

Welcome and thanks for using Unity Simulation. Unity Simulation enables product developers, researchers, and engineers to easily and efficiently run thousands of instances of parameterized Unity builds in batch in the cloud. Unity Simulation allows you to parameterize a Unity project in ways that will change from run to run. You can also specify simulation output data necessary for your end application, whether that be the generation of training data for machine learning, the testing and validation of AI algorithms, or the evaluation and optimization of modeled systems. With Unity Simulation, there is no need to install and manage batch computing software or server clusters that you use to run your jobs, allowing you to focus on analyzing results and solving problems. 

We hope you enjoy using the service, if you have any questions please open a thread in [the forum](https://forum.unity.com/forums/unity-simulation.407/) or contact support at simulation-help@unity3d.com.

Sign up [here](https://dashboard.unity3d.com/metered-billing/marketplace/products/c20ae33a-6301-4bd3-9b17-4874027a4ed4) to start for free now!

## Pre-Requisites to installing Unity Simulation

You should install a compatible version of Unity that is listed below. Please make sure to include linux build support in your installation.

- Unity Account
- Unity Cloud Project
- Unity version >= 2018.4 (>= 2019.3 for [SRP](https://docs.unity3d.com/Manual/ScriptableRenderPipeline.html) support)
- Supported Graphics APIs: OpenGL (upto 3.3)
- Supported platforms: Windows10+ and OS X 10.13+
- Linux build support required

Please refer to the [Installing pre-requisites guide](doc/requirements.md) for a step by side guide to installing the above pre-requisites.

## Getting started with Unity Simulation

| Section | Description |
|---|---|
|[Sign Up for Access](https://dashboard.unity3d.com/metered-billing/marketplace/products/c20ae33a-6301-4bd3-9b17-4874027a4ed4)| Get access to start for free now |
|[Unity Simulation Concepts](doc/taxonomy.md) | Unity Simulation Concepts|
|[QuickStart tutorial](doc/quickstart.md) | How to get started with Unity Simulation - A walkthrough |
|[Sample Smart-Camera-Outdoor](https://github.com/Unity-Technologies/Unity-Simulation-Smart-Camera-Outdoor) | Sample unity project demonstrating usage of simulation packages for outdoor smart camera usecases.
|[Sample Roll-A-Ball tutorial](https://github.com/Unity-Technologies/Unity-Simulation-RollABall) | Sample unity project integrated with the Unity Simulation SDK|
|[Warehouse Robotics](https://assetstore.unity.com/packages/essentials/tutorial-projects/unity-simulation-sample-project-warehouse-robot-176606)| Sample unity warehouse robotics project demonstrating usage of Unity Simulation and Perception SDK. 

## Developing a Simulation
| Section | Description |
|---|---|
|[Unity Simulation SDK](doc/integrate.md) | Developing with the Unity Simulation SDK|
|[Unity Linux build](doc/build.md) | How to make a Linux build|
|[Linux Build Testing](doc/testing.md) | Testing Linux build locally|

## How-to Guides
| Section | Description |
|---|---|
|[Use Case How-tos](doc/use-cases/use-cases.md) | Example use cases and how to implement them.|
|[Simultaneous Capture](doc/simultaneous-capture.md)|How to simultaneously log data and capture an image.|
|[Cloud Data Transfer](doc/data-transfer.md) | Transfer USim data to your cloud. |
|[Troubleshooting](doc/troubleshooting.md) | Troubleshooting common issues.|

## Current Limitations
- Currently USim only supports CPU based rendering via [XVFB](https://www.x.org/releases/X11R7.6/doc/man/man1/Xvfb.1.xhtml) which means it is restricted to OpenGL version supported by mesa software renderer [llvmpipe](https://docs.mesa3d.org/gallium/drivers/llvmpipe.html) (i.e upto version 3.3).
- Rendering pipelines: With OpenGL Gfx API you can run your project with built-in/legacy rendering pipeline or [Universal Rendering Pipeline](https://docs.unity3d.com/Packages/com.unity.render-pipelines.universal@8.2/manual/index.html). [High Definition Rendering Pipeline](https://docs.unity3d.com/Packages/com.unity.render-pipelines.high-definition@7.1/manual/Getting-started-with-HDRP.html) (HDRP) is currently not supported as it requires Vulkan or DirectX Gfx API.
- Texture compression [supported by Unity](https://docs.unity3d.com/Manual/texture-compression-formats.html) is not supported by the software renderer used in the cloud (llvmpipe).
- Simulation runtime in the cloud needs to be LinuxStandalone.
- Running simulation workload with GPUs is not currently supported.

## Reference

| Section | Description |
|---|---|
|[API Docs](https://api.simulation.unity3d.com/swagger/index.html)| Documentation for using the Simulation API |
|[CLI commands](doc/cli.md) | command descriptions for the CLI |
