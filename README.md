# creating-swap-arch-linux
Certainly, I can guide you through setting up an 8 GB swap file on Arch Linux. Here are the steps:

1. First, let's remove the existing swapfile:

```bash
sudo rm /swapfile
```

2. Now, let's create the swapfile with COW disabled, but without trying to set the compression property:

```bash
sudo truncate -s 0 /swapfile
sudo chattr +C /swapfile
sudo fallocate -l 2G /swapfile
sudo chmod 600 /swapfile
sudo mkswap /swapfile
```

3. Try to activate the swap:

```bash
sudo swapon /swapfile
```

4. If successful, make it permanent by adding to /etc/fstab:

```bash
echo '/swapfile none swap defaults 0 0' | sudo tee -a /etc/fstab
```

5. To verify that COW is disabled for the swapfile, you can use:

```bash
lsattr /swapfile
```

You should see the 'C' attribute listed, indicating that COW is disabled.

If you still encounter issues, we might need to consider creating a separate swap partition instead. Would you like to try these steps first, or should we explore the partition option?
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
