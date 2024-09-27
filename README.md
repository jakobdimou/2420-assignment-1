# 2420-assignment-1
## Introduction
In this tutorial, you will be setting up an Arch Linux environment through DigitalOcean. This guide aims to demonstrate:
- [Generating SSH keys on your local machine](#generating-an-ssh-key-on-your-local-machine)
- [Uploading a custom Arch Linux image](#uploading-a-custom-arch-linux-image-to-digitalocean)
- [Setting up a droplet running Arch Linux](#droplet)
- [Using a cloud-init file to automate initial setup tasks](#cloudinit)

## Generating an SSH key on your local machine
Creating an SSH key will be necessary to connect to and authenticate a droplet on DigitalOcean.

As most of you are probably on windows, create a .ssh directory in your home directory if you haven't yet.


To find your home directory you can type the command:
```
cd ~
```
This command will create the .ssh directory:
```
mkdir .ssh
```

If the creation of the .ssh directory is successful, you can then use this command to generate an SSH key:
```
ssh-keygen -t ed25519 -f ~/.ssh/name-of-key -C "leave your comment here"
```
For Windows users, the command above may not work in PowerShell due to the `~` expansion, so enter the full path.
```
ssh-keygen -t ed25519 -f C:\Users\your-windows-user\.ssh\name-of-key -C "leave your comment here"
```
### Command Breakdown
- `ssh-keygen`: Create the SSH key
- `-t ed25519`: Dictate the type of encryption used, which in this case is ed25519
- `-f ~/.ssh/name-of-key`: Specify the filepath
- `-C "leave your comment here"`: Leave a comment

Replace `name-of-key` with a name for your key, and replace `"leave your comment here"` with a comment to help you identify the key later, like your email address or something helpful.

After running the command, you will be asked to enter a passphrase. This is optional but provides added security. Keep in mind you will need to remember this password everytime you use the SSH key.

> Note: If something went wrong, try going through all the steps again and confirm the steps were followed correctly.

## Adding your public SSH key to DigitalOcean

The public SSH key file will be located in the `~/.ssh` directory and has a `.pub` extension. For example, if you named your key `kim-dokja`, the public key file would be `~/.ssh/kim-dokja.pub`.

You could just just open the file in notepad and copy the content from there, or you could directly copy it to your clipboard using the terminal

An example in PowerShell would be:

```
Get-Content C:\Users\your-windows-user\.ssh\name-of-key.pub | Set-Clipboard
```

The copied content should look something like this:
 ```
 ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAIL4h5e1uV1cS0+MHoWk5V5hiPUbpDq323jXhm4KnKBub johnsmith@gmail.com
 ```

 ### Adding the public key to your DigitalOcean account
 
 - Head to the **settings page** from the dropdown menu
 - Click on the **security tab** and press the **"Add SSH key"** button.
 - Add your public key in the **"SSH Key content"** area
 - Give the SSH key a name for better organization
 - Press **"Add SSH key"** to finalize the process

 **✧Congratulations!✧** You have now generated an SSH key and added it to your DigitalOcean account.


## Uploading a custom Arch Linux image to DigitalOcean

To start, an Arch linux image will need to be downloaded. The file can be found [here](https://gitlab.archlinux.org/archlinux/arch-boxes/-/packages/).

Download the file from the latest **images** package that contains **"cloud-img"** and ends with **".qcow2"**

### On the DigitalOcean website

- Click on the **"Backups & Snapshots"** page from the **"Manage"** dropdown menu
- Click on the blue **"Upload Image"** button
- Select the image file you just downloaded

>Note: When uploading the Arch Linux image, make sure to select **Arch Linux** as the distribution and **San Francisco 3** for the datacenter region as it is the closest server to Vancouver, BC

It should look something like this when the upload has completed:

![arch linux upload complete](images/archlinux.png)


## Using a cloud-init file to automate initial setup tasks