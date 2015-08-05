# Setting up your ACMS account for git and github ssh access

## Pairs: Separate sessions for each partner ON THE SAME SCREEN.

The following steps need to be done for each pair partner.  That means you need a terminal session for each pair partner, and a github.com browser session for each partner, like this:

![SPIS multiple sessions](/images/SPIS_multiple_sessions.png)

But you do NOT need two computers for this.  Here's how to do this on the same computer.

Suppose the first pair partner is spis15aa, and the second pair partner is spis15bb.  
Further, suppose that spis15aa is the one logged into the computer, but
you need to do these steps for both partner spis15aa and partner spis15bb.

First the spis15aa partner can open a terminal, and a browser window and log into github.com.

Now, the spis15bb partner also needs her/his own (a) terminal window and (b) browser login to github.com.

Here's how to do that:

* Open a second terminal window.  In that window, type: ssh `spis15bb@ieng6-240.ucsd.edu`.   The spis15bb partner can type in her/his password.
* In your web browser, open a "Incognito" or "Private Browsing" window.   In that window, the second partner can log in to his/her github.com account.

Now, without having to log out and log back in completely, you can have both a terminal window and github.com browser window
for both  partner one, and partner two.

BE SURE TO DO ALL OF THE STEPS BELOW, SEPARATELY, FOR EACH PARTNER.



## Step 1: Set up an ssh key on your ACMS account.

We will set up a public/private key pair on your ACMS account.  


The idea of a public/private key pair is that you give away your public key, 
and you keep your private key a secret.   This allows anyone with your 
public key to **know that *you* are you** without you having to type in a password 
(as long as your private key stays secret).



To generate a public/private key pair: Open a terminal session, and type the `ssh-keygen` command.

You will be asked a series of questions.  For each question, just press the enter/return key (to accept the default option.)

That will look like this:

```
[spis15t7@ieng6-240]:~:353$ ssh-keygen
Generating public/private rsa key pair.
Enter file in which to save the key (/home/linux/ieng6/spis15/spis15t7/.ssh/id_rsa): 
Enter passphrase (empty for no passphrase): 
Enter same passphrase again: 
Your identification has been saved in /home/linux/ieng6/spis15/spis15t7/.ssh/id_rsa.
Your public key has been saved in /home/linux/ieng6/spis15/spis15t7/.ssh/id_rsa.pub.
The key fingerprint is:
de:8f:c0:d8:69:bc:82:e9:06:e9:30:25:42:16:bc:1c spis15t7@ieng6-240
The key's randomart image is:
+--[ RSA 2048]----+
|...              |
| E               |
|+ o              |
|oo.              |
|.o .    S        |
|o o    * o       |
| + . o. O .      |
|  . + .. o o     |
|   o.  .. . .    |
+-----------------+
[spis15t7@ieng6-240]:~:354$ 
```

The effect of that is to create two files in a hidden directory of your account called `.ssh`.  

If you type `cd` to your home directory, and `ls` at your terminal prompt, you will not see this directory.  Example:

```
[spis15t7@ieng6-240]:~:354$ cd
[spis15t7@ieng6-240]:~:355$ ls
C:\nppdf32Log\debuglog.txt  Music      Videos     index.html    pygithub
Desktop                     Pictures   github     index.html.1  spis
Documents                   Public     hello.py   lesson2.py
Downloads                   Templates  hello.py~  lesson2.py~
[spis15t7@ieng6-240]:~:356$
```

But if you use `ls -al` you WILL see the `.ssh` directory along with many other hidden directories. Find the `.ssh` in the 
list below, then try it on your own account.  

```
[spis15t7@ieng6-240]:~:356$ ls -a 
.              .gconfd          .pki                        Pictures
..             .gnome2          .procmailrc                 Public
.ICEauthority  .gnome2_private  .pulse                      Templates
.Xauthority    .gnote           .pulse-cookie               Videos
.abrt          .gnupg           .ssh                        github
.bash_history  .gstreamer-0.10  .vnc                        hello.py
.bash_profile  .gtk-bookmarks   .xsession-errors            hello.py~
.bashrc        .gvfs            .xsession-errors.old        index.html
.cache         .imsettings.log  .zprofile                   index.html.1
.config        .kshrc           .zshenv                     lesson2.py
.cshrc         .local           .zshrc                      lesson2.py~
.dbus          .locallogin      C:\nppdf32Log\debuglog.txt  pygithub
.emacs.d       .login           Desktop                     spis
.esd_auth      .modulesbegenv   Documents
.fontconfig    .mozilla         Downloads
.gconf         .nautilus        Music
[spis15t7@ieng6-240]:~:357$ 
```

# Step 2: cd into your .ssh directory

Now, type the command `cd ~/.ssh` at the Terminal prompt.

Then do `ls`

You should see two files `id_rsa` and `id_rsa.pub` as follows.  (If you see other files, don't worry)

```
[spis15t7@ieng6-240]:.ssh:361$ cd ~/.ssh
[spis15t7@ieng6-240]:.ssh:362$ ls
id_rsa  id_rsa.pub
[spis15t7@ieng6-240]:.ssh:363$ 
```

You want to now look at the contents of `id_rsa.pub`, which is your **public** key.  That is the one you are going to share with github.com.   (The contents of `id_rsa` are your private key, which you do NOT share. )

To see the contents of id_rsa.pub, we use the cat command:

```
[spis15t7@ieng6-240]:.ssh:363$ cat id_rsa.pub
ssh-rsa AAAAB3NzaC1yc2EAAAABIwAAAQEA1yTFW/PkiZCebbR9EqkduGCApKwW7uy7CZ1ThomgG+xZsVgWWIMirzkNJbahxwwEVIH0Hj+irID3ICkH8o60T3QiMk1v5VJSVFaKdqtiZXFQapYR2Rwln1wf2XXBCT/cdVWif9usiS5vLqtno74/dpKCEiELjGSHdpFTyFoF3ZHR6plFYA2/iX4XWDrDJwG/Qwf+SBd0uzIy7CpFrQK+9kMWDrK2jUGhd0goYPQu2LCgHxnu8R041M5ooSUE79seE+64gVcjoSfPJwdKhZdwy2zjYvKKz0CM4w3ysPbOpr1FkT6MnlhN3dyJBFA+BjmtXGVDNl7a5yjtY9QzORILfQ== spis15t7@ieng6-240
[spis15t7@ieng6-240]:.ssh:364$ 
```

Your public key will look different, but similar.  You are now going to to do a "copy/paste" of that key into a page of github.com.   Our next step is to navigate to the correct page of github.com to enter that key.


## Go to the github.com settings menu, then SSH keys


<table border="1">
<tr>
<td>
<img src="/images/ssh-key-setup/01-github-settings-menu.png" alt="github.com settings menu" width="200" >
</td>
<td><img src="/images/ssh-key-setup/02-ssh-keys-menu-option.png" alt="Choose the ssh keys menu option" width="200" >
</td>
</tr>
</table>

## Click Add SSH key

As shown here:


![Click Add SSH key](/images/ssh-key-setup/03-click-Add-SSH-key.png)

## Copy your SSH public key

As shown here.  Be careful to get the whole key, but nothing more than the key.  Don't include the shell prompts or the cat command.

![Copy your ssh public key](/images/ssh-key-setup/04-copy-your-ssh-public-key.png)

![paste in your ssh public key](/images/ssh-key-setup/05-paste-in-your-ssh-public-key.png)

Github may ask for your password as shown here:

![github asks for your password](/images/ssh-key-setup/06-github-asks-for-your-password.png)

Then you should get a message that your key was added:

![github confirms that key was added](/images/ssh-key-setup/07-SPIS-key-added.png)
