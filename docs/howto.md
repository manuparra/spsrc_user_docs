
[TOC]

# How-to guide

Here we gather a collection of how-to notes with the aim of helping users to self-manage their virtual machines.

# User management

Initially there is only one preconfigured user account on the virtual machine, the **spsrc** user,
with privileges to create new accounts for your collaborators.

## Change your default password

Run the following command on a terminal and follow instructions:
```
passwd
```

## Create a user account

Open a terminal and run the following commands:
```
# Generate a new password hash:
openssl passwd

# Create a new account:
sudo useradd --password "<output-from-previous-command>" --gid spsrc-group --create-home --shell /bin/bash <collaborator>
```
For example:
```
# Create a new account:
sudo useradd --password "<output-from-previous-command>" --gid spsrc-group --create-home --shell /bin/bash john
```

.. caution::
   Please configure a password with less than 8 characters. We have experimented issues with longer passwords.

## Delete a user account

You can delete a user account using the userdel command:
```
sudo userdel <collaborator> --remove
```
For example:
```
sudo userdel john --remove
```

# Software installation

All users are granted with **sudo** privileges to use the operating system package manager
(i.e. **apt-get** in Ubuntu, and **yum/dnf** in Centos7/8) to install packages via the official
repositories. 

# SSH access

SSH access into virtual machines is only allowed via public-key authentication.

## Create your own public SSH key

For general information about how SSH authentication works, please visit:

[https://www.ssh.com/ssh/key/](https://www.ssh.com/ssh/key/)

If you have already created a public SSH key on your computer, it should be available in:

```
# list your SSH keys
ls -al $HOME/.ssh
```

If the command above works, you just need to check whether your SSH key is loaded with:

```
# check whether your SSH keys are loaded
ssh-add -L
```

That should print out all the SSH public keys that are already loaded in you terminal
so just pick one to configure your SSH access to the virtual machine.

If the `ssh-add -L` command did not return any output, please execute `ssh-add` or 
`ssh-add ./path/to/private/key/` to load it. More information
[here](https://www.ssh.com/ssh/agent#adding-ssh-keys-to-the-agent)

Please note that both **private** and **public** SSH keys are located in the `$HOME/.ssh` folder.
Public keys are usually stored in files ending with the **.pub** extension. If you have one,
you can either email it to us via ska-itsupport 'at' iaa.csic.es or follow steps in the next
section to configure SSH access yourself via Guacamole.

.. danger::
   Please make sure you only share public SSH (files ending in .pub) with others.

If the `ls -al $HOME/.ssh` command above fails, it is very likely that you haven not configured
SSH keys yet. To do so please use the `ssh-keygen` command:

```
# create a new SSH key pair
ssh-keygen
```

Follow instructions on your terminal and for more information please visit:

[https://www.ssh.com/ssh/keygen/](https://www.ssh.com/ssh/keygen/)

If all went well you should have a new file ending in **.pub** under the `$HOME/.ssh` folder.
Then, feel free to email us a copy of your **.pub** file to ska-itsupport 'at' iaa.csic.es
so we configure your SSH access or follow steps in the next section if you have access to Guacamole.

## Add your public SSH key to access your virtual machine

If you have access to the virtual machine via [Guacamole](#remote-desktop-guacamole) then you can
add your public SSH key to your account yourself. Please open a terminal and try these steps:

```
# go to your home folder
cd

# create an .ssh folder if it doesn't exist
mkdir -p .ssh

# configure permissions
chmod 0700 -R .ssh

# now cd into the .ssh folder
cd .ssh

# create an authorized file and add your public SSH key
vi authorized_keys

# configure permissions
chmod 0600 authorized_keys
```

You should now be able to login with your SSH keypair. If you have problems, please send your
public key to ska-itsupport 'at' iaa.csic.es and we will configure SSH access for you.

# Transfer data

We suggest using [FileZilla](https://filezilla-project.org/download.php?type=client) to transfer data
in and out of the virtual machine.

Transfers will only be possible via public SSH authentication. Here are instructions on how to
configure FileZilla to work with SSH keys: 

[https://wiki.filezilla-project.org/Howto](https://wiki.filezilla-project.org/Howto)

Please send your public SSH key to ska-itsupport 'at' iaa.csic.es so we can configure it for you.

# Remote desktop: Guacamole

When a project requires access to a remote desktop we preconfigure virtual machines with
[Apache Guacamole](https://guacamole.apache.org).

## Working with the clipboard in Guacamole

Using the clipboard in Guacamole is not intuitive. If you are planning to use the clipboard a lot,
and the information you are going to work with is available online (i.e. via a web browser), we then
recommend you to open firefox to copy/paste as usual inside the virtual machine.

If, on the other hand, you need to copy/paste between your workstation and the virtual machine, then
you will have to use the Guacamole menu. On the tab where you have Guacamole working, press **Ctrl+Alt+Shift** 
and the menu appears on the left:

![](images/guac-clipboard.png)

You will see the Guacamole clipboard that will be used as an intermediate buffer between your workstation
and the virtual machine:

* Copy/paste from your workstation to the virtual machine: 1) first copy the text into the clipboard
as usual in your workstation; 2) open the Guacamole menu with **Ctrl+Alt+Shift** and paste your text
into the Guacamole clipboard; 3) the text is now available inside the virtual machine clipboard and
you can paste it as expected with **Ctrl+V**

* Copy/paste from the virtual machine to your workstation: 1) use **Ctrl+C** inside the virtual machine
to copy text as usual; 2) open the Guacamole menu with **Ctrl+Alt+Shift** and copied text automatically
appears in the Guacamole clipboard; 3) you can now copy from there into your workstation's clipboard.

## How to change your password in Guacamole

Press **Ctrl+Alt+Shift** to open the Guacamole menu, first click on your username (**spsrc** on the
example image) and then on **Settings**:

![](images/guac-change-pass.png)

Then go to **Preferences** and follow instructions to change your password:

![](images/guac-change-pwd.png)

## How to add a new user in Guacamole

Go to the menu on the top-right and click on **Settings**:

![](images/guac-menu-user.png)

Then go to **Users** and click on **New User**:

![](images/guac-add-user-1.png)

Enter a username and password for the new user:

![](images/guac-add-user-2.png)

Scroll down and check the following and click on **Save**:

* Permissions/Change own password
* Connections/RDP

![](images/guac-add-user-3.png)

## How to change your locale in Guacamole

Depending on your system's [locale](https://en.wikipedia.org/wiki/Locale_(computer_software))
you may find issues while typing text inside the virtual machine via Guacamole. Check
whether you have the correct configuration in Guacamole by following the steps below.

Go to the menu on the top-right and click on **Settings**:

![](images/guac-menu-user.png)

Then go to **Connections** and click on **RDP**:

![](images/guac-locale-1.png)

Now look for the **Basic Settings** section and choose the correct **keyboard layout**:

![](images/guac-locale-2.png)

Do not forget to scroll down and click on **Save**.

# Conda

[Conda](https://conda.io) is a package manager that help you find and install software
packages without having administrator privileges.

Below are the steps to get a basic conda installation working with Python 3. Open
a terminal on your virtual machine and run the following commands:

```
# Go to a working directory to install conda
mkdir test
cd test

# Download installer
curl -O https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh

# Install conda in the "conda-install" folder
bash Miniconda3-latest-Linux-x86_64.sh -b -p conda-install

# Activate conda
source conda-install/etc/profile.d/conda.sh

# Create a basic environment with the latest Python 3
conda create -n py3env python=3

# Activate the "py3env":
conda activate py3env

# check it with
which python
python --version

# "pip" is also available:
which pip

# To leave the environment, type:
conda deactivate
```
Conda environments are great for managing the dependencies on your projects
and it helps you improve the reproducibility of your code. For more information
about conda, please visit:

https://docs.conda.io/projects/conda/en/latest/user-guide/getting-started.html

## Install JupyterLab with Conda

Here we describe the steps to install JupyterLab into its own conda environment:

```
# Follow steps above to install conda.
# Then create a conda environment for JupyterLab:
conda create -n jupyterlab -c conda-forge jupyterlab -y
conda activate jupyterlab
jupyter lab --ip=0.0.0.0 --port=<port-number>
```
JupyterLab will print out the URL to connect to your session.
