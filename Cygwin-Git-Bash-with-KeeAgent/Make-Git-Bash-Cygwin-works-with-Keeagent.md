# How to make Git Bash and Cygwin works with KeeAgent on Windows.

_I didn't find an obvious way to make Git Bash (and Cygwin as well) works with KeeAgent. Since my SSH keys are stored only within KeePass, I needed to use KeeAgent and without the use of temporary files. Also, this was made on Windows 10, so the tutorial may vary a bit for older versions of Windows._

#### This tutorial assume that you've already done that :
- Installed Git;
- Installed KeePass;
- Installed the KeeAgent plugin with KeePass;
- Set up an entry in KeePass with KeeAgent configured to use the attached SSH private key;
- Configured KeeAgent to make that SSH key available (_in the Tools -> KeeAgent menu_). This means that you are able to establish an SSH connection with Putty, for example.

## Summary
1. Create a MSYS socket file.
2. Add the location of the MSYS socket file to the environment variable named SSH_AUTH_SOCK.

### MSYS Socket file
One can simply create a socket file by following these steps :

1. Click on the menu **Tools -> Options**.
2. Navigate to the **KeeAgent** tab.
3. Now you have to choose either one of the two following options. For me, the first option worked out. We will use the options in the bottom section, named **Cygwin/MSYS integration**  
   - Cygwin compatible socket :
      1. Check the first box. It is named **Create Cygwin compatible socket file (works with some versions of MSYS)**.
      2. Click on the **Browse** button.
      3. Go to the folder which you want the socket file to be.
      4. Write a name for your socket, like **cygwin.socket**. Now, this will create the socket file automatically when you clik on the **Save** button.
   - msysGit compatible socket :
      1. Check the second box. It is named **Create msysGit compatible socket file**.
      2. Click on the **Browse** button.
      3. Go to the folder which you want the socket file to be.
      4. Write a name for your socket, like **cygwin.socket**. Now, this will create the socket file automatically when you clik on the **Save** button.
5. Now, before closing the **options** window, copy the path of the socket file you've created. We'll need it later.
6. Click the **OK** button.

### Creating the environment variable SSH_AUTH_SOCK
Now, you don't actually needs to interact within Cygwin/Git Bash to set up your environment variable. Actually, you do it in Windows, as Cygwin/Git Bash copy Windows' environment variables when they start. =)

1. Open the **file explorer**. This can be done by pressing _Win+E_ or by opening a random folder.
2. Right click on **This PC**, then click on **Properties**.
3. Click on **Advanced system settings**.
4. Navigate to the **Advanced** tab.
5. Click on the **Environment variables**.
6. Create a new **System variable** with the following variable name : **SSH_AUTH_SOCK**
7. Now, in **Value**, copy the path we made while creating the socket file.

By now, this should be working. If it doesn't, you could need to use the other type of socket, as specified earlier.

This tutorial is inspired by the documentation that I've found on the subject :
- [The closed GitHub issue about using KeeAgent with Git Bash](https://github.com/dlech/KeeAgent/issues/114)
- [KeeAgent documentation about socket files](http://lechnology.com/software/keeagent/usage/tips-and-tricks/#cygwin-and-msys)
