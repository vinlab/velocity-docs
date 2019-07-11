# Velocity Docs
### Veracode's CI Agnostic onboarding and static scanning tool.

## Velocity Overview
Velocity (by Veracode Innovation Labs) is a small, statically compiled executable requiring minimal configuration and enables bulk onboarding of customer application into the Veracode Platform.

## Features

- Cross Platform (currently Linux/OS X)
- CI Agnostic
- Automatic application identification via Git metadata
- Automatic binary/module identification and upload
- Supports Gradle, Maven, NPM, and Yarn (more coming)

## How it Works
Velocity runs after the build step inside CI.  When run, Velocity does the following:
1. The Velocity shell script will compare the latest Velocity version.  If it exist locally, it's run.  If not it is downloaded and cached locally.
2. Identifies the Git URl and branch of the application. This is used to match up the current app with the App Profile on the Veraode Platform.
3. Examines the local folder to identify the build system used (Mavne/NPM/etc).
4. Based on the build system, Velocity will automatically package up required files and upload them to the Veracode Platform.
5. When all files are uploaded, it will initiate a prescan.

At the moment full scans are not automatically initiated, but this can be done manually from the Platform.

## Supported OS/Architectures

Velocity currently support 64bit Linux and OS X.  Builds exist for ARM and Windows but these have not been fully tested.  Please contact Jason Nichols (jnichols@veracode.com) if you're interested in testing these out.

## Requirements
Velocity is statically compiled and has no runtime dependencies other than the following:
- Curl and Bash (for Velocity Script)
- Git (for application identification)


## Running Velocity

Start by setting up Veracode username/password credentials for Velocity. Ensure that you have username/password and not API tokens. In your environment set the following:

```
> export VERACODE_USERNAME=<username>
> export VERACODE_PASSWORD=<username>
```

Then, within any folder you wish to scan or as part of your post-build step in your CI, run the following:
```
> curl https://veracode-velocity.s3.amazonaws.com/velocity.sh | sh
```

This will invoke the Velocity script and execute Velocity in the current folder.  If you wish to scan a particular or sub-folder of the current directory, you can pass that as an argument:

```
> curl https://veracode-velocity.s3.amazonaws.com/velocity.sh | sh  -s -- </folder/to/scan>
```

TODO Topics:
- Installation/Setup
  - Jenkins
  - TravisCI
  - CircleCI
  - Bamboo


