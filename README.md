# Dimorf
Dimorf is a ransomware using 256-bit AES with a self-destructing, randomly generated key for Linux OS´s 

## Why Dimorf?
- This name came as inspiration from the Mr. Robot, where the main character is a morphine user, the pharmaceutical name of morphine is dimorf, in parts the name was also inspired by the [LKM Rootkit Diamorphine](https://github.com/m0nad/Diamorphine). Diamorphine is the pharmaceutical name for Heroin.

## Features
- <b>check_os:</b> checks if the operating system is a Linux type and if Python is running on version 3. If both conditions are true, the main function is called.

- <b>find_and_encrypt:</b> searches for files in a given path <b>(path)</b> and checks if these files have a specific extension <b>(ext_files)</b>. If a file has a valid extension, the function checks that it is not a hidden file <b>(starts with ".")</b>. If a file meets these conditions, the function checks whether the current user has read, write, and access permissions for that file. If this is the case, the file is renamed (adding tmp_ext to the end of the file name) to validate that there isn't some process on the operating system using the file. Then, the function starts a file encryption process using AES <b>(Advanced Encryption Standard)</b> and overwrites the original file with the encrypted version. If there is an error in the file renaming operation, the function checks if there is any process running that is using that file and, if so, kills that process. If the current user does not have read, write or file access permissions. In this case, the function tries to change the permissions of the file to 0o644 at octal base <b>(which means that the owner of the file has read and write permissions and all other users have read permissions only)</b>. If the permission change is successful, the function proceeds with the process of encrypting the file, overwriting the original file with the encrypted version and removing the original file. Otherwise, the function does nothing with the file and moves on to the next file in the list of found files.

- <b>main:</b> starts by checking whether the current user is the root user, i.e. the system administrative user. If the current user is root, the code checks to see if the ROOT_PATH environment variable has already been set. If it has not been set, the code sets the ROOT_PATH environment variable to the value passed to the main() function as the ROOT_PATH argument. After that, the find_files() function is called with the specified arguments. if all conditions pass. The USER_DIR variable it now takes the value of the ROOT_PATH environment variable, otherwise USER_DIR remains as the current user's home directory.
