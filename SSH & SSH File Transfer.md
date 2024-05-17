

To copy a folder from one Ubuntu machine to another using SSH, you can use the following command:

Code

Code copied!

```
scp -r /path/to/local/directory user@remotehost:/path/to/remote/directory
```

This will copy the entire directory, including all of its contents, to the remote machine.

For example, to copy the directory `/home/user/my_folder` to the remote machine `192.168.1.100` in the directory `/home/user/`, you would use the following command:

Code

```
scp -r /home/user/my_folder user@192.168.1.100:/home/user/
```

You will be prompted to enter the password for the user account on the remote machine. Once you have entered the password, the copy process will begin.

If you are copying a large directory, it may take some time for the copy process to complete. You can monitor the progress of the copy by using the `-v` option.

For example, to copy the directory `/home/user/my_folder` to the remote machine `192.168.1.100` in the directory `/home/user/` and monitor the progress of the copy, you would use the following command:

Code

```
scp -rv /home/user/my_folder user@192.168.1.100:/home/user/
```

Once the copy process is complete, you will be able to access the copied directory on the remote machine by logging in to the remote machine and navigating to the directory where the files were copied.


