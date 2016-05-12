# How to run multiple SSH keys on Bitbucket and GitHub

In this tutorial I'll create and run two different SSH keys on the same service (BitBucket in this case, but also works for other services such as GitHub). One key for my personal projects and another for my work related projects.

First of all I'll create my personal key:

`$ ssh-keygen -t rsa -C "myemail@mypersonalemail.com"`

I'll name it *personal* and save it to my `~/.ssh` hidden folder. You can either enter in the .ssh folder and run the terminal in there or pass the path when *ssh-keygen* asks you the "file in which to save the key". The folder location is likely to be `C:\Users\your-username\.ssh`.

Run this process again to create your work key and register the keys to your [Bitbucket](https://confluence.atlassian.com/bitbucket/use-deployment-keys-294486051.html) or
[GitHub](https://help.github.com/articles/adding-a-new-ssh-key-to-your-github-account/) account. Now in ~/.ssh I'll open (or create) the `config` file and type the following configuration:
```
Host bitbucketPersonal
  HostName bitbucket.org
  User git
  IdentityFile ~/.ssh/personal

Host bitbucketWork
  HostName bitbucket.org
  User git
  IdentityFile ~/.ssh/work
```

To test the work so far, I'll clone an existing repository. The clone URL 
would usually be `$ git clone git@bitbucket.org:your-user/your-repo.git`.

As it is a personal project I'll change this URL slightly to `$ git clone git@bitbucketPersonal:your-user/your-repo.git`. Being *bitbucketPersonal* the name of the host given at the config file.

I'll now set my git configuration for this specific repository, setting my name and email. This information will be later used
in the commit history of the repository. Inside the repo type `$ git config user.name "Your Name"`and `$ git config user.email myemail@mypersonalemail.com`.

And that's it! :)

Source:

[Generating a new SSH key and adding it to the ssh-agent](https://help.github.com/articles/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent/)

[Configure multiple SSH identities for GitBash, Mac OSX, & Linux](https://confluence.atlassian.com/bitbucket/configure-multiple-ssh-identities-for-gitbash-mac-osx-linux-271943168.html)

[Como ter duas chaves SSH no Linux](http://www.brunonardini.com.br/desenv-back-end/como-ter-duas-chaves-ssh-no-linux)

[Multiple SSH Keys settings for different github account](https://gist.github.com/jexchan/2351996)

[Use different SSH keys for different accounts on the same Git hosting](http://stackoverflow.com/questions/20353564/use-different-ssh-keys-for-different-accounts-on-the-same-git-hosting/)

[Storing git config as part of the repository](http://stackoverflow.com/questions/18329621/storing-git-config-as-part-of-the-repository)

[Setting your email in Git](https://help.github.com/articles/setting-your-email-in-git/)

[First-Time Git Setup](https://git-scm.com/book/en/v2/Getting-Started-First-Time-Git-Setup)

[Git Configuration](https://git-scm.com/book/en/v2/Customizing-Git-Git-Configuration)

