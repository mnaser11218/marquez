# README KSM

Documents dev/build changes to the base Marquez project and custom KSM developer setup.

FYI docker image versions are managed in the `docker/up.sh` script. Right now "-ksm" is appended to the last version before fork; eventually there will be a separate version system (and perhaps project/component names), but for now doing a `docker ps` and seeing *-ksm* is a quick visual cue that a component was locally built and not pulled from Docker Hub for the original project.

## DEV Setup form Marquez on WSL

### Install WSL

[LearnMicrosoft Install Instructions](https://learn.microsoft.com/en-us/windows/wsl/install)

WSL can also be installed via the Microsoft Store, although it would be prudent to make sure to get the latest (not guaranteed with the store) by going into Powershell and running `wsl --update`

Open Ubuntu and update all packages:

```
sudo apt update
sudo apt upgrade
```

### Install Docker

More UNIX-savvy people may want to consider installing and using docker completely in the WSL. The Windows option with Docker Desktop can be easier to manage thanks to the good GUI, but it makes broader changes to the workstation that (in my case @jkominetz) can result in problems like the WSL hanging for long periods of time.

#### Docker Desktop

An alternative is to use Docker Desktop. Having a GUI to manage the docker installation can be very nice, but there are some potential trade-offs. This raises some licensing issues when used for work, and Docker Desktop going wrong can be very hard to troubleshoot and fix.

#### Docker Ubuntu

Be careful with Googling for how to do this; old pages can result in an obsolete docker install especially if the instructions are generic for Ubuntu and not specific to the older package set the default WSL Ubuntu seems to prefer. The best thing to do is add Docker's apt repo and pull the latest docker available:

[Install Docker on Ubuntu by Docker](https://docs.docker.com/engine/install/ubuntu/)

### Install SDKMAN (WSL)

This great little tool is very easy to install (via curl!). It does require zip and unzip, so install those via apt if not already present. The primary purpose here is to manage the java SDK and gradle versions. That can get really messy when different projects require different versions or distros of tools. It does much more than java and gradle, so check out the full list on the web page.

[SDKMAN One-liner Installation and Website](https://sdkman.io/)
```
sudo apt update
sudo apt upgrade
sudo apt install zip unzip
```

### Install JDK and Gradle (WSL)

At forking the project recommended Java 17. A more recent Java will probably work too. The project uses the Eclipse version of OpenJDK, so for consistency stake use the most current Temurin 17 release.

```
sdk install java 17.0.15-tem
sdk install gradle 8.14.1
```

The most recent gradle (as of 2025-06-04) works with the project, but the apt-repo version (4.4) does not. If gradle isn't working, check your version.

### Working with WSL project

#### IntelliJ

For the API, written in Java, IntelliJ is probably the best choice of IDE.

Once the WSL is fully set up, IntelliJ should "just work" with projects hosted on the WSL. I have only confirmed so far that I can load the project (Navigate and open the build.gradle file on the Linux filesystem), run a build from the gradle panel, edit files (and manage them in git).

#### Visual Studio Code

For the JavaScript GUI component, vscode was recommended. In theory, this will also work on Java, unix, docker, and whatever with the right plugins, so having vscode available for general purpose work is also recommended.

The best option is to just use `code` from Ubuntu directly, but I'm guessing that the windows install will do the right thing once vscode server (is automagically?) installed in your wsl.