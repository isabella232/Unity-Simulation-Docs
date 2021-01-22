# Troubleshooting

## Data Generation
All data saved by the Unity Simulation SDK during a running simulation in the Editor is saved to a local directory and should be referenced to determine that the correct data is being generated, in the correct quantity, and in the correct form.

Attaching the following `DataCapturePath.cs` to any game object that is active when the scene begins will print the path where the Unity Simulation SDK will save all data for a particular run.
```csharp
using Unity.AI.DXCore;
using UnityEngine;

public class DataCapturePath : MonoBehaviour
{
    void Start()
    {
        // Print path where data will be saved by Unity Simulation SDK
        Debug.Log(Application.persistentDataPath + "/" + Configuration.Instance.GetAttemptId());
    }
}
```

## Linux Build
Please reference the [Local Testing](testing.md) guide for information on how to test a Linux build locally.

## SDK Integration

#### Using ML-Agents and Unity Simulation/Playtesting SDK together.

Both ML-Agents and Unity Simulation/Playtesting include the assembly ```system.interactive.async.dll```.
This will cause the build system to throw the following exception when building, and if both packages are present.
`PrecompiledAssemblyException: Multiple precompiled assemblies with the same name System.Interactive.Async.dll included for the current platform. Only one assembly with the same name is allowed per platform.`
This error is clearable and ignorable, but will occur each time you build.

This will be resolved soon™, but as a work around for now, you can delete one of the two copies of the assembly in either package after import.

#### Some cameras are rendering out grey images

Secondary cameras need to render into a render texture, and that RT may need a depth attachment.
The primary camera uses the display backbuffer with a depth attachment, but secondary cameras need to render into something.
Adding a render target will solve this issue. If your objects in the scene use shaders with depth testing enabled, then make sure that the RT has depth enabled.


#### UnityPlayer.so file not found

```
 error while loading shared libraries: UnityPlayer.so: cannot open shared object file: No such file or directory
```

Starting 2019.2, LinuxStandalone build generates a UnityPlayer.so file along with the Data directory. You need to zip the project build along with UnityPlayer.so file before uploading it to USim.

## CLI commands

#### Too many projects when using `activate project`

The `activate project` command accepts an optional argument for the Unity project id. \
```bash
usim activate project xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx
```
This Unity Project ID value may be retrieved from:
* [Unity Developer Dashboard](https://developer.cloud.unity3d.com/projects/).
* Combine the `get projects` command with command-line tools such as `less` or redirecting the output to a file with `>`.
```bash
usim get projects > my_projects.txt
OR
usim get projects | less
```

## macOS Gatekeeper

Apple has [information and instructions](https://support.apple.com/en-us/HT202491) for Gatekeeper issues.

If you see pop-ups such as `"usim" cannot be opened because the developer cannot be verified"`, that's the Gatekeeper being triggered. Scenarios can be downloading the quick start assets using a browser, extracting the files using a non-native archive utility, etc., as long as macOS finds the files downloaded may be or have been altered.

Using the `cURL` command to download, and the `unzip` command, or the native `Archive Utility.app` to decompress is recommended:

```
curl -Lo unity_simulation_bundle.zip https://github.com/Unity-Technologies/Unity-Simulation-Docs/releases/download/v20210111/unity_simulation_bundle.zip
unzip unity_simulation_bundle.zip -d unity_simulation_bundle
```

#### Validating checksums

Our release notes will have checksums included for macOS releases. You can verify that the `usim` executable is in tact by comparing the checksum of the file. Produce a checksum with the `shasum -a 256 usim` command and compare the output with the checksum included in the release notes.

#### Quarantine attribute

macOS adds a quarantine attribute that may prevent launching usim. If this occurs you should first [validate the checksum](#Validating-checksums). You can remove the quarantine attribute with `xattr -rd com.apple.quarantine /path/to/usim`.

#### Allow terminal to load libraries
Error `not valid for use in process using Library Validation: library load disallowed by system policy`

The macOS Terminal app settings may need to be set to allow loading libraries. Navigate to System Preferences and then:

Security & privacy -> Privacy tab -> Developer tools -> make sure terminal checkbox is checked


