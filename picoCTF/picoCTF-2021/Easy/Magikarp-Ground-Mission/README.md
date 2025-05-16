# Magikarp Ground Mission

## Description

Do you know how to move between directories and read files in the shell? Start the container, `ssh` to it, and then `ls` once connected to begin. Login via `ssh` as `ctf-player` with the password, `ee388b88`

## Approach

After `ssh`ing into the container and listing the files we see the first part of a flag and some instructions for the 2nd flag

![1of3](images/1o3.png)

Next we need to go to the root of the filesystem using `cd /`. Theres the next part of the flag and some more instructions

![2of3](images/2o3.png)

It's telling us to go to `~` which is our home directory. We can get there with `cd` by itself or `cd ~`

![3of3](images/3o3.png)

Now we can combine all parts to get the flag!!
