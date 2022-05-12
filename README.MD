# DUO Git Repos

Open your terminal and cd into `~/.ssh`

inside the .ssh folder
check to see if you have a config file by typing in the terminal 
`ls -a`

For this to work we will use **User1** (default) and **User2**

run `ssh-keygen -t rsa -b 4096 -C "user1@email.com"` with user 1's email

You will be asked the follow:

**Enter file in which to save the key (/Users/someusername/.ssh/id_rsa).**

You can press **enter** on the first one if you wish to use the **default** `id_rsa`

run `ssh-keygen -t rsa -b 4096 -C "user2@email.com"` with user 2's email but when  encountering Enter file in which to save the key for the second user's email use a new name for example `id_rsa_user2`



when you do `ls -a` you should have something like this:

```
id_rsa
id_rsa.pub
id_rsa_user2
id_rsa_user2.pub
```

Next you have to add the SSH keys to your SSH-agent

```
ssh-add -K ~/.ssh/id_rsa
ssh-add -K ~/.ssh/id_rsa_user2
```

Inside the .ssh folder check to see if there is a `config` file if you don't have one you can create one with `touch config`. This allows you to have some options in ssh. 

Open the config file in a text editor and you will insert the following:

```
# User1
Host github.com
  HostName github.com
  User git
  IdentityFile ~/.ssh/id_rsa
  
# User2
Host github.com-user2   
  HostName github.com
  User git
  IdentityFile ~/.ssh/id_rsa_user2
```

Inside the terminal, for the global github settings you can use your user1 (default):

```
$ git config --global user.name "githubUser1"
$ git config --global user.email "user1@email.com"
```



#### Register your keys to the respective GitHub accounts.

- Follow these [steps](https://help.github.com/articles/adding-a-new-ssh-key-to-your-github-account/) to do so.



Cloning down github repos will be of the following:

 If you are cloning for user1
`git clone git@github.com-user1:user1/your-repo-name.git your-repo-name_user1`

 If you are cloning for user2

`git clone git@github.com-user1:user2/your-repo-name.git your-repo-name_user2`



For each repo you can change.

`git config --add user.email someone@domain.com` to add/override user email in given repo
`git config --unset user.email someone@domain.com` to remove user email entry in given repo



