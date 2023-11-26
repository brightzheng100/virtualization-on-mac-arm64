# Virtualization On Mac ARM64 CPU

Before M1 chip, my favarite virtualization tool on Mac was [VirtualBox](https://www.virtualbox.org/).

Unfortunately, VirtualBox is a x86 and AMD64/Intel64 virtualization product so it's born with AMD64/Intel64.
It's NOT possible to work in Mac with ARM64 chips (e.g. M1, M2).

So, what are the best _free_ virtualization tools if you're with ARM64 CPU?

Here are some personal experiments / sharings for you.

## **TL'DR**

- [UTM](https://mac.getutm.app/) might be the best tool when you need a **simulator** where you can run VMs with either AMD64/x86_64 or ARM64 CPU. So you have all the choices.
- [VMware Fusion Player](https://www.vmware.com/sg/products/fusion.html) is a great tool to run native CPU-based VMs, which is ARM64 when you're with Mac + M1/M2 chips. VMware Fusion has out-of-the-box [Vagrant](https://www.vagrantup.com/) plugin so you can streamline your development & testing process with automated VM bootstrapping experience.

## UTM

### Install UTM

There are two simple steps to install UTM:

1. Download the latest [UTM.dmg](https://github.com/utmapp/UTM/releases/latest/download/UTM.dmg) file and double click to open the installation page;
2. Drag the UTM.app icon into Applications icon and it's done.

![UTM Installation](screenshots/utm-installation.png)

Once you've opened the UTM app, you should be able to see a very neat screen like this:

![UTM Overview](screenshots/utm-overview.png)

### Get Started with UTM Gallary

You may click the "Browse UTM Gallary" button which will open your default browser and navigate to UTM's [gallery](https://mac.getutm.app/gallery/) where you can see a list of UTM community curated VMs.

Let's pick "ArchLinux" as an example to walk you through.

Firstly, navigate to the [UTM Gallery](https://mac.getutm.app/gallery/) and you should be able to see ArchLinux icon, click it and click download button:

![UTM Gallery](screenshots/utm-archlinux-in-gallery.png)
![UTM Gallery ArchLinux](screenshots/utm-archlinux-download.png)

Then unzip the downloaded .zip file and you would get a .utm file, say "ArchLinux.utm".

Open UTM app and click "Create a New Virtual Machine" button:
![UTM Create VM](screenshots/utm-create-vm.png)

Click the "Open..." button and locate the "ArchLinux.utm" file and click Open.

Now the ArchLinux should be in your VM list and get ready:
![UTM ArchLinux Added](screenshots/utm-archlinux-in-list.png)

Click the big start button to start the VM.
Use the `root/root` to login and it's all set in 1 minute or so:
![UTM ArchLinux Bootstrapped](screenshots/utm-archlinux-started.png)

### Get Started with ISO Files

It's common that you want to create the VM from an existing ISO file, or your desired VM is not available from UTM Gallery.

In this case, you can easily create a VM from an ISO in UTM.

You can always click the "+" button to start creating a VM:
![UTM Start](screenshots/utm-start.png)

You may notice that there are two options: **Virtualize** and **Emulate**.
Let me quickly explain what they are, the pros and cons that you should be aware of.

- **Virtualize**. It's similar to VirtualBox on x86_64/AMD64 CPU. It's much faster than "Emulate" but can only run the native CPU architecture. So if you're with ARM64 CPU on Mac with M1/M2 chips, you can run VMs with ARM64 CPU only.
- **Emulate**. It's slower (but actually is still acceptable), but you can run many supported CPU architectures as well. So if you want to run x64_86/AMD64 CPU on Mac with M1/M2 chips, this is the only option to proceed.

So depending on which VM you want to run while deciding which way to get started.

For example, it's common that I want to test things on an Ubuntu VM with x64_86/AMD64 CPU, I'll start with **Emulate**.
Click **Emulate** to proceed, and pick Linux, among 3 options: Windows, Linux, and Other.

![UTM Start OS Type](screenshots/utm-start-os-type.png)

What we need now is to browse and pick your desired ISO file.
In my case, it's "ubuntu-20.04-live-server-amd64.iso". Click Continue.

![UTM Start Linux](screenshots/utm-start-linux.png)

As we have chosen "Emulate" option to start with, in the Harware step, we have the chance to select any supported CPU architecture where x86_64 is one of the options.
You may tune the CPU and Memory too to suit your needs. Click Continue.

![UTM Start Hardware](screenshots/utm-start-hardware.png)
![UTM START Hardware CPU Architectures](screenshots/utm-start-hardware-cpus.png)

In the Storage step, you can specify the Storage. I'd just click Continue.

![UTM Start Storage](screenshots/utm-start-storage.png)

Now, you can specify the Shared Directory to mount to the VM from the host.
I'd ignore it and click Continue.

![UTM Start Shared Directory](screenshots/utm-start-shared-storage.png)

Now it comes to Summary step, let's name it "Ubuntu 20" or any desired name you want.

![UTM Start Summary](screenshots/utm-start-summary.png)

Once it's done, the "Ubuntu 20" should be added into the VM list:

![UTM Start Complete](screenshots/utm-start-complete.png)

Now, click the big start button and you should see the lovely Ubuntu installation screen:

![UTM Start Installation](screenshots/utm-start-installation.png)

Go and install it to be your Ubuntu VM, with x86_64/AMD64 CPU, on Mac with native M1/M2 chips!

## VMware Fusion Player

### Download VMware Fusion Player

VMware Fusion has two versions:
- Fusion Pro. This is a purchasable commercial product.
- Fusion Player. This is a free product for personal use.

In the VMware Fusion for Mac Download page, [here](https://www.vmware.com/sg/products/fusion/fusion-evaluation.html), click "REGISTER FOR A PERSONAL USE LICENSE" under "Fusion 13 Player for macOS 12+" as of writing.

You may click "I Have an Account" to login if you already have an VMware account, or click "Create an Account" to create a new free account.

![VMware Fusion Landing Page](screenshots/fusion-landing-page.png)

Log into it with your VMware account:

![VMware Login](screenshots/fusion-vmware-login.png)

Once you've logged in, generate the free personal license and download the binary:

![VMware Fusion Download](screenshots/fusion-download.png)

### Install VMware Fusion Player

The downloaded file is a normal .dmg file, double click to start the installation process.

![VMware Fusion Installation](screenshots/fusion-installation.png)

Simply follow the installation guide and VMware Fusion Player should be easily installed.

###  Get Started with VMware Fusion Player

Open VMware Fusion Player, the landing page is very neat (and empty) at first.

![VMware Fusion App Landing](screenshots/fusion-app-landing.png)

Click "+" drop down button and select "New...", a popup window should be displayed:

![VMware Fusion App New VM - Select Method](screenshots/fusion-new-vm-method.png)

In the "Select the Installation Method", there are 3 options:
- Install from disc or image
- Create a custom virtual machine
- Get Windows from Microsoft

Let's pick "Install from disc or image" and drag an Ubuntu ISO file into it.

Please note that we can only download and use ARM64 ISO images, for example "ubuntu-20.04.4-live-server-**arm64**.iso", and x64_86/AMD64 ISO images won't be supported as explained in the "TL'DR" section at the beginning.

Drag and drop the "ubuntu-20.04.4-live-server-arm64.iso" file into it to start:

![VMware Fusion App New VM - Start](screenshots/fusion-new-vm-start.png)

Click "Continue" to proceed:

![VMware Fusion App New VM - Configure](screenshots/fusion-new-vm-configure.png)

There are some default settings, if you're okay with it, just click "Finish" to finish the VM creation process.

Or click the "Customize Settings" to customize the settings. Once you select so, it will prompt you to save the VM first and then prompt you with Settings' UI:

![VMware Fusion App New VM - Customize](screenshots/fusion-new-vm-customize.png)

You may explore the settings to fulfil your advanced needs.

For me, I'd ignore and close the prompt window and click the start button.

![VMware Fusion App New VM - Done](screenshots/fusion-new-vm-done.png)

And you should see the familiar Ubuntu VM installation screen. Feel free to install the VM with your desired configuration to be your VM.

![VMware Fusion App New VM - OS Installation](screenshots/fusion-new-vm-os-installation.png)

> Important Note:
> 1. Use Ctrl + Command to release the mouse if you want to be back to your Mac
> 2. You may create folders in VMware Fusion Player to better organize your VMs


### Vagrant Integration

VMware Fusion has out-of-the-box Vagrant support.

#### Get ready with Vagrant

Let's assume you already have Vagrant installed. If not, run this to install:

```sh
# Install vagrant with brew
$ brew install vagrant

# Check the version installed
$ vagrant --version
Vagrant 2.4.0
```

#### Install necessary packages for the integration

Installation of the Vagrant VMware provider requires two steps.

Firstly, the "Vagrant VMware Utility" must be installed.

This can be done by downloading and installing the correct system package from the "Vagrant VMware Utility" downloads page, [here](https://developer.hashicorp.com/vagrant/install/vmware).

Please note that the "Vagrant VMware Utility" .dmg file is for AMD64 only so Rosetta on your Mac must have been installed -- I guess everyone of us must have done so. Please follow [this Apple KB](https://support.apple.com/en-sg/HT211861) to install Rosetta.

Secondly, we need to install the Vagrant VMware provider plugin:

```sh
$ vagrant plugin install vagrant-vmware-desktop
```

#### Hello World

Let's look at the "Hello World" level Vagrantfile, which is available in "./vagrant/Vagrantfile.HelloWorld":

```ruby
Vagrant.configure("2") do |config|
    config.vm.box = "sloopstash/ubuntu-22-04"
    config.vm.provider "vmware_desktop" do |vp|
        vp.memory = "2048"
        vp.cpus = "1"
  end
end
```

And have a try:

```sh
$ VAGRANT_CWD=./vagrant/hello-world vagrant up
```

OUTPUT:

```log
Bringing machine 'default' up with 'vmware_desktop' provider...
==> default: Box 'sloopstash/ubuntu-22-04' could not be found. Attempting to find and install...
    default: Box Provider: vmware_desktop, vmware_fusion, vmware_workstation
    default: Box Version: >= 0
==> default: Loading metadata for box 'sloopstash/ubuntu-22-04'
    default: URL: https://vagrantcloud.com/api/v2/vagrant/sloopstash/ubuntu-22-04
==> default: Adding box 'sloopstash/ubuntu-22-04' (v2.1.1) for provider: vmware_desktop
    default: Downloading: https://vagrantcloud.com/sloopstash/boxes/ubuntu-22-04/versions/2.1.1/providers/vmware_desktop/unknown/vagrant.box
==> default: Successfully added box 'sloopstash/ubuntu-22-04' (v2.1.1) for 'vmware_desktop'!
==> default: Cloning VMware VM: 'sloopstash/ubuntu-22-04'. This can take some time...
==> default: Checking if box 'sloopstash/ubuntu-22-04' version '2.1.1' is up to date...
==> default: Verifying vmnet devices are healthy...
==> default: Preparing network adapters...
==> default: Starting the VMware VM...
==> default: Waiting for the VM to receive an address...
==> default: Forwarding ports...
    default: -- 22 => 2222
==> default: Waiting for machine to boot. This may take a few minutes...
    default: SSH address: 127.0.0.1:2222
    default: SSH username: vagrant
    default: SSH auth method: private key
    default:
    default: Vagrant insecure key detected. Vagrant will automatically replace
    default: this with a newly generated keypair for better security.
    default:
    default: Inserting generated public key within guest...
    default: Removing insecure key from the guest if it's present...
    default: Key inserted! Disconnecting and reconnecting using new SSH key...
==> default: Machine booted and ready!
==> default: Configuring network adapters within the VM...
==> default: Waiting for HGFS to become available...
==> default: Enabling and configuring shared folders...
    default: -- /Users/brightzheng/workspaces/tools/virtualization-on-mac-arm64/vagrant/hello-world: /vagrant
```

We now can use `vagrant ssh` to SSH into the VM:

```sh
$ VAGRANT_CWD=./vagrant/hello-world vagrant ssh
```

OUTPUT:

```console
Welcome to Ubuntu 22.04.2 LTS (GNU/Linux 5.15.0-76-generic aarch64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/advantage

  System information as of Sun Nov 26 05:46:43 PM UTC 2023

  System load:  0.51513671875      Processes:             235
  Usage of /:   12.1% of 29.82GB   Users logged in:       0
  Memory usage: 11%                IPv4 address for eth0: 172.16.25.134
  Swap usage:   0%


This system is built by the Bento project by Chef Software
More information can be found at https://github.com/chef/bento

vagrant@vagrant:~$ cat /etc/os-release
PRETTY_NAME="Ubuntu 22.04.2 LTS"
NAME="Ubuntu"
VERSION_ID="22.04"
VERSION="22.04.2 LTS (Jammy Jellyfish)"
VERSION_CODENAME=jammy
ID=ubuntu
ID_LIKE=debian
HOME_URL="https://www.ubuntu.com/"
SUPPORT_URL="https://help.ubuntu.com/"
BUG_REPORT_URL="https://bugs.launchpad.net/ubuntu/"
PRIVACY_POLICY_URL="https://www.ubuntu.com/legal/terms-and-policies/privacy-policy"
UBUNTU_CODENAME=jammy

vagrant@vagrant:~$ uname -a
Linux vagrant 5.15.0-76-generic #83-Ubuntu SMP Thu Jun 15 19:21:56 UTC 2023 aarch64 aarch64 aarch64 GNU/Linux
vagrant@vagrant:~$
```

Please note that the provisioned VM isn't listed in VMware Fusion Player by default.
But we can change the such default behaviour by updating the `Vagrantfile` with `vp.gui = true` to explicitly bring the VM into VMware Fusion Player's VM list: 

```ruby
Vagrant.configure("2") do |config|
    config.vm.box = "sloopstash/ubuntu-22-04"
    config.vm.provider "vmware_desktop" do |vp|
        vp.memory = "2048"
        vp.cpus = "1"
        vp.gui = true
  end
end
```

Then run `vagrant up`:

```sh
$ VAGRANT_CWD=./vagrant/hello-world vagrant up
```

And you should see the VM listed in the VMware Fusion Player UI:

![VMware Fusion Player with Vagrant Integrated](screenshots/fusion-vagrant-integrated.png)

Once the VM's mission is completed, we can shut it down with:

```sh
$ VAGRANT_CWD=./vagrant/hello-world vagrant halt
```

OUTPUT:

```log
==> default: Attempting graceful shutdown of VM...
```

Or even destroy it, with:

```sh
$ VAGRANT_CWD=./vagrant/hello-world vagrant destroy
```

OUTPUT:

```log
    default: Are you sure you want to destroy the 'default' VM? [y/N] y
==> default: Deleting the VM...
```

#### References

There are quite some good references to explore further for the Vagrant and VMware Fusion Player integration:
- Hashcorp Vagrant's VMware plugin configuration page: https://developer.hashicorp.com/vagrant/docs/providers/vmware/configuration
- sloopstash's kickstart-linux GitHub repo: https://github.com/sloopstash/kickstart-linux
