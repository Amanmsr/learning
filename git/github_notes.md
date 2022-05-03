### Pull Requests
You create a separate branch  
You make changes to the newly created branch  
You submit a pull request asking the original branch owner to review your changes and 'pull' them into your branch.  
A pull request has a title and a description  
We can do GUI diff within Github to compare 'main' with 'pr_branch'  
The created branch is deleted when the pull request is merged into the 'main' branch.  

### Github with CLI git
* connecting over HTTPS
* connecting over SSH

Github deletes SSH key if they are not used for one year.  
If we change our computer we need to generate new keys and delete the old ones from Github.  

**Adding ssh key to github**  
we need to add public key to github  
open the public key file (.pub) and copy the key  
github.com -> settings -> SSH and GPG keys -> New SSH key  
provide a title and then the key itself  
title should give info about the machine on which the key was generated so that when that machine is no longer valid (ex: changing linux distro)  
we can delete that particular public key from github  
confirm github password  

### SSH
we need to generate SSH keys and if we pull the repo on a new computer we cannot push anything since we don't have the keys.  
If someone gets access to our computer they will be able to push everything onto the repo since private key is on our computer.  
To protect against this we need a passphrase which we have to enter each time we want to push to repo.  

```
* ls -alh ~/.ssh (check for existing keys)
* ssh-keygen -t ed25519 -C "amanmsr99@gmail.com" (creates a key pair using ed25519 algorithm with the comment "amanmsr99@gmail.com")
* The generated keys will be in ~/.ssh and be named id_ed25519 and id_ed25519.pub
* ssh-add ~/.ssh/id_ed25519 (add private key to ssh-agent so that passphrase is not required each time)
```
*NOTE*: during ssh-keygen we can control the location of the keys (default is ~/.ssh)  


