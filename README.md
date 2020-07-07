# Unity Simulation Documentation

Welcome and thanks for using Unity Simulation. Unity Simulation enables product developers, researchers, and engineers to easily and efficiently run thousands of instances of parameterized Unity builds in batch in the cloud. Unity Simulation allows you to parameterize a Unity project in ways that will change from run to run. You can also specify simulation output data necessary for your end application, whether that be the generation of training data for machine learning, the testing and validation of AI algorithms, or the evaluation and optimization of modeled systems. With Unity Simulation, there is no need to install and manage batch computing software or server clusters that you use to run your jobs, allowing you to focus on analyzing results and solving problems. 

We hope you enjoy using the service, if you have any questions please open a thread in [the forum](https://forum.unity.com/forums/unity-simulation.407/) or contact support at simulation-help@unity3d.com.

Sign up [here](https://dashboard.unity3d.com/metered-billing/marketplace/products/c20ae33a-6301-4bd3-9b17-4874027a4ed4) to get access to free credits now!

## Pre-Requisites to installing Unity Simulation

You should install a compatible version of Unity that is listed below. Please make sure to include linux build support in your installation.

- Unity Account
- Unity Cloud Project
- Unity version >= 2018.4 (>= 2019.3 for [SRP](https://docs.unity3d.com/Manual/ScriptableRenderPipeline.html) support)
- Supported platforms: Windows10+ and OS X 10.13+
- Linux build support required

Please refer to the [Installing pre-requisites guide](doc/requirements.md) for a step by side guide to installing the above pre-requisites.

## Getting started with Unity Simulation

| Section | Description |
|---|---|
|[Sign Up for Access](https://dashboard.unity3d.com/metered-billing/marketplace/products/c20ae33a-6301-4bd3-9b17-4874027a4ed4)| Get access to free credits for our service |
|[Unity Simulation Concepts](doc/taxonomy.md) | Unity Simulation Concepts|
|[QuickStart tutorial](doc/quickstart.md) | How to get started with Unity Simulation - A walkthrough |
|[Sample Smart-Camera-Outdoor](https://github.com/Unity-Technologies/Unity-Simulation-Smart-Camera-Outdoor) | Sample unity project demonstrating usage of simulation packages for outdoor smart camera usecases.
|[Sample Roll-A-Ball tutorial](https://github.com/Unity-Technologies/Unity-Simulation-RollABall) | Sample unity project integrated with the Unity Simulation SDK|

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
|[Troubleshooting](doc/troubleshooting.md) | Troubleshooting common issues.|

## Reference

| Section | Description |
|---|---|
|[API Docs](https://api.simulation.unity3d.com/swagger/index.html)| Documentation for using the Simulation API |
|[CLI commands](doc/cli.md) | command descriptions for the CLI |
|[Tiers](doc/usage-tiers.md)| How tiers affect your resource allowance and usage |
