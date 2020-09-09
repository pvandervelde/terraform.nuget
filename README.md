# terraform.nuget

![Nuget](https://img.shields.io/nuget/v/Terraform.Windows.x64?style=for-the-badge)

This repository contains the scripts used to create a [NuGet package](https://www.nuget.org/packages/Terraform.Windows.x64/) containing the Windows binaries for [Terraform](https://www.terraform.io/).

The NuGet packages produced from this repository will be versioned with the version of Terraform that they contain, e.g. the NuGet package with version `0.12.26` will contain Terraform version `0.12.26`.

In some cases the NuGet package will have a fourth number, e.g. `0.12.26.2`. In this case the fourth number indicates a re-release of the NuGet package for a given version of Terraform. This may be done to fix issues with the previous version of the NuGet package.


## How to build

During the build process the Terraform binary with the version specified in the `version.xml` file will be downloaded, the file hash compared and then unzipped and placed in a NuGet package.

At the end of the build process the NuGet package can be found in the `build/deploy` folder in the workspace.

Note that the `version.xml` file contains 4 version number parts. Only the first three (`VersionMajor`, `VersionMinor` and `VersionPatch`) are used to find the correct version of Terraform. The fourth number, `VersionBuild` exists to allow multiple NuGet packages to be created with the same version of Terraform, in case there are changes to the NuGet package itself.

To execute a local build you need MsBuild installed and have the NuGet [command line application](https://www.nuget.org/downloads) on the PATH.

From the root of the repository workspace issue the following command:

`msbuild entrypoint.msbuild /t:build`

This will pull down the required tools, download the Terraform artefact with the correct version, verify the file hashes, unzip the artefact and place it inside a NuGet package.
