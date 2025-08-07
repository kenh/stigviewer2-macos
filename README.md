# STIGViewer 2 for MacOS X

This is a version of the Java-based DISA STIGViewer (as of this
writing, STIGViewer 2.18) packaged with the necessary Java runtime
environment, all organized into a friendly application bundle suitable
for direct installation in your `Applications` folder.  Included in this
repository is all of the tooling I use to generate the app bundle and
the associated installer.

## How to Use

If you don't want to build it yourself, navigate to the
[GitHub release page](https://github.com/kenh/stigviewer2-macos/releases)
and you will find the latest release provided as a signed and notarized
Installer package.  Install that the normal way, and you should be good to
go.  This package includes JREs for both Intel and Apple Silicon architectures.

## How to Build Your Own Installer

First, acquire appropriate Java Runtime Environments (JREs) for both
Intel and Apple Silicon.  As of this writing, I am using JDK 24 as
provided by Bellsoft; you can download these from the
[Bellsoft Download Page](https://bell-sw.com/pages/downloads/).  Note
that you need the **Full** JRE, not the Standard JRE; the Full JRE
included JavaFX which is needed by the STIGViewer.  Download the
gzipped tar files and place them in the `jre` directory in a checked-out
copy of the repository.  Note that currently `build-package` is expecting
a naming similar to the Bellsoft JREs; specifically, the tar files should
have in the filename the string `jre` and the Intel and Apple Silicon
JREs should have `amd64` and `aarch64` in the filename, respectively.

In the repo the `build-package` script does all of the work of building
the app bundle, creating the Installer package, and signing and notarizing
the package.  To sign the package you will need an Apple Developer ID
Application AND a Developer ID Installer signing identities.  By default
`build-package will look through your Keychain to find those identities.
To notarize the package you will have to supply your notarization username
(which is the email associated with your Apple developer account) in
the `NOTARYUSER` environment variable.

`build-package` supports the following environment variables

| Variable | Description |
| --- | --- |
| `NOTARYUSER` | The username used to authenticate to the notarization service.  This is mandatory |
| `NOTARYPW` | The Keychain profile name containing a stored notarization password, typically stored with `notarytool store-credentials`.  Defaults to `Notarization`. |
| `APPCERT` | A string used to search for a valid code signing certificate. Defaults to `Developer ID Application:` |
| `INSTCERT` | A string used to to search for a valid Installer signing certificate. Defaults to `Developer ID Installer:\ |
| `SKIPSIGN` | If set, the app bundle and Installer will not be signed |
| `SKIPNOTARY` | If set, notarization will be skipped |

## What about STIGViewer 3?

Hopefully, eventually ...

## Author

* **Ken Hornstein** - [kenh@cmf.nrl.navy.mil](mailto:kenh@cmf.nrl.navy.mil)
