# creating-swap-arch-linux
Certainly, I can guide you through setting up an 8 GB swap file on Arch Linux. Here are the steps:



```bash
# 1. Create an 8GB swap file
sudo fallocate -l 8G /swapfile

# 2. Set correct permissions (readable only by root)
sudo chmod 600 /swapfile

# 3. Format the file as swap
sudo mkswap /swapfile

# 4. Enable the swap file
sudo swapon /swapfile

# 5. Make the swap file permanent by adding it to /etc/fstab
echo '/swapfile none swap defaults 0 0' | sudo tee -a /etc/fstab

# 6. Verify the swap is active
free -h

```

Here's a breakdown of these steps:

1. We create an 8GB swap file using `fallocate`.
2. We set the permissions so only root can read and write to it.
3. We format the file as swap space.
4. We enable the swap file.
5. We add an entry to /etc/fstab to make the swap persistent across reboots.
6. Finally, we verify that the swap is active.

After running these commands, you should have an 8GB swap file set up and active on your Arch Linux system.


# removing the swap 
To delete the swap file we just created on Arch Linux, you'll need to follow these steps:



```bash
# 1. Turn off the swap
sudo swapoff /swapfile

# 2. Remove the swap file entry from /etc/fstab
sudo sed -i '/swapfile/d' /etc/fstab

# 3. Delete the swap file
sudo rm /swapfile

# 4. Verify the swap has been removed
free -h

```

Here's an explanation of these steps:

1. First, we turn off the swap using the `swapoff` command. This ensures the system stops using the swap file.

2. Next, we remove the swap file entry from /etc/fstab. This prevents the system from trying to use the swap file on next boot. The `sed` command searches for any line containing 'swapfile' and deletes it.

3. We then delete the actual swap file using the `rm` command.

4. Finally, we verify that the swap has been removed by checking the system's memory information.

After running these commands, the swap file will be completely removed from your system.

Remember to run these commands with caution, especially if you've made any custom modifications to your swap setup. Always double-check before deleting system files.
