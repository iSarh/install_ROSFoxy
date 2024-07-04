This guide is derived from the official Noetic setup page, which can be found here:

https://docs.ros.org/en/foxy/Installation/Ubuntu-Install-Debians.html

# install ROS FOXY on ubuntu

Before starting to install ROS, you need to :

**download VirtualBox:** https://www.virtualbox.org/wiki/Downloads

**download Ubuntu 24.04 ( Install it on Virtual Box ):** https://ubuntu.com/download/desktop

if VirtualBox and Ubuntu are not familiar to you, here is some help to do that:
https://youtu.be/x5MhydijWmc?feature=shared

## install ROS Foxy

First of all, you need to set the locale so you can simply type ```locale``` on the terminal.

 ```bash
locale
```
![photo_2024-07-04_14-29-42](https://github.com/iSarh/install_ROSFoxy/assets/63901303/52ee3806-663b-4268-a228-637998929739)

If you don't have this then execute:

```bash
sudo apt update && sudo apt install locales
sudo locale-gen en_US en_US.UTF-8
sudo update-locale LC_ALL=en_US.UTF-8 LANG=en_US.UTF-8
export LANG=en_US.UTF-8
```
```bash
sudo locale-gen en_US en_US.UTF-8
```
```bash
sudo update-locale LC_ALL=en_US.UTF-8 LANG=en_US.UTF-8
```
```bash
export LANG=en_US.UTF-8
```

# Setup Sources
ROS2 is not directly available with sudo apt

First, ensure that the Ubuntu Universe repository is enabled.

```bash
sudo apt install software-properties-common
sudo add-apt-repository universe
```
 
Now add the ROS 2 GPG key with apt.

```bash
sudo apt update && sudo apt install curl -y
sudo curl -sSL https://raw.githubusercontent.com/ros/rosdistro/master/ros.key -o /usr/share/keyrings/ros-archive-keyring.gpg
```
Then add the repository to your sources list.

```bash
echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/ros-archive-keyring.gpg] http://packages.ros.org/ros2/ubuntu $(. /etc/os-release && echo $UBUNTU_CODENAME) main" | sudo tee /etc/apt/sources.list.d/ros2.list > /dev/null
```
# Install ROS packages

Update your apt repository caches after setting up the repositories.

```bash
sudo apt update
```
> [!NOTE]
> You may face an error
> E: Unmet dependencies. Try 'apt --fix-broken install' with no packages (or specify a solution) LibreOffice
> 
> To fix it run:
> ```bash
> sudo apt -o Dpkg::Options::="--force-overwrite" --fix-broken install
> ```

Now install the packages.

You have 3 options here, so choose the one that suits you:

- Desktop Install (Recommended): ROS, RViz, demos, tutorials.
  
  ```bash
  sudo apt install ros-foxy-desktop python3-argcomplete
  ```
- ROS-Base Install (Bare Bones): Communication libraries, message packages, command line tools. No GUI tools.
  
  ```bash
  sudo apt install ros-foxy-ros-base python3-argcomplete
  ```
- Development tools: Compilers and other tools to build ROS packages
  ```bash
  sudo apt install ros-dev-tools
  ```
# Environment setup
  
Set up your environment by sourcing the following file

```bash
source /opt/ros/foxy/setup.bash
```
# Testing
In one terminal, source the setup file and then run a C++ talker:
```bash
source /opt/ros/foxy/setup.bash
ros2 run demo_nodes_cpp talker
```
In another terminal source the setup file and then run a Python listener:

```bash
source /opt/ros/foxy/setup.bash
ros2 run demo_nodes_py listener
```

You should see the talker saying that it’s Publishing 'Hello World 'and the listener saying I heard 'Hello World'


![Screenshot 2024-07-04 152641](https://github.com/iSarh/install_ROSFoxy/assets/63901303/e76a86db-ed47-4074-965c-e89da0e6f4ff)








