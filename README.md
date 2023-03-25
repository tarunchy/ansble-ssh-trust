# Ansible Trust Setup

This guide explains how to establish trust between an Ansible controller and a target VM for SSH using passwordless authentication with public key cryptography.

## Generate an SSH key pair

On the Ansible controller machine, generate an SSH key pair (if you haven't already) using the following command:

ssh-keygen -t ed25519 -C "your_email@example.com"

Replace "your_email@example.com" with your actual email address or another identifier.

This command generates a new Ed25519 key pair. You'll be prompted to enter a file name for the key pair and an optional passphrase for additional security.

## Copy the public key to the target VM

Use the `ssh-copy-id` command to copy the public key to the target VM:

ssh-copy-id -i ~/.ssh/id_ed25519.pub user@target-vm-ip

Replace `user` with the target VM's username and `target-vm-ip` with the target VM's IP address or hostname.

You'll be prompted for the target VM's password. The `ssh-copy-id` command will append the public key to the `~/.ssh/authorized_keys` file on the target VM.

## Test the passwordless SSH connection

Test the passwordless SSH connection with the following command:

ssh user@target-vm-ip

Replace `user` with the target VM's username and `target-vm-ip` with the target VM's IP address or hostname.

If everything is set up correctly, you should be able to connect to the target VM without entering a password.

After establishing passwordless SSH authentication, Ansible will be able to connect to the target VM without requiring a password. Make sure to update your Ansible inventory file with the target VM's information, specifying the correct user and IP address or hostname.
