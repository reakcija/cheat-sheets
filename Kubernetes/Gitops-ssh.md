
Dodavanje ssh kljuceva na mac, rad sa vise naloga:

https://medium.com/@viviennediegoencarnacion/manage-github-and-gitlab-accounts-on-single-machine-with-ssh-keys-on-mac-43fda49b7c8d

To create private and public SSH pairs for your personal, and work accounts, run:

ssh-keygen -t rsa -C "personal@mail.com" -f ~/.ssh/id_rsa_gitlab  
ssh-keygen -t rsa -C "personal@mail.com" -f ~/.ssh/id_rsa_github

These will produce four different files namely:

~/.ssh/id_rsa_github  
~/.ssh/id_rsa_github.pub  
~/.ssh/id_rsa_gitlab  
~/.ssh/id_rsa_gitlab.pub

# Step 2. Add SSH keys to Github, and Gitlab

**Github**  
Copy corresponding public key of your Gitlab account  
`pbcopy < ~/.ssh/id_rsa_github.pub`

Logon to your Github account. Then go to  
`Settings > SSH and GPG Keys > New SSH key`

Paste the public key on the `Key`, and edit the `Title` part as you please.

![](https://miro.medium.com/v2/resize:fit:700/1*jmsHUf2Kprpkrt5hQHpk-Q.png)

Adding SSH keys on GitHub

**Gitlab  
**Copy corresponding public key of your Gitlab account  
`pbcopy < ~/.ssh/id_rsa_gitlab.pub`

Logon to your Gitlab account. Then go to `Settings > SSH Keys`

Paste the public key on the `Key`, and edit the `Title` part as you please.

![](https://miro.medium.com/v2/resize:fit:700/1*vuCcJfAkiPwkbBfcQCmQ0Q.png)

Adding SSH keys on GitLab

# Step 3: Register SSH Keys with the ssh-agent

Register all SSH keys on your local machine using the ssh-agent

ssh-add ~/.ssh/id_rsa_github  
ssh-add ~/.ssh/id_rsa_gitlab

# Step 4: Editing Config File

Create a configuration file that will add the different SSH keys for all online repositories and emails that we created earlier

touch ~/.ssh/config    // Creates config file if it does not exist  
vi ~/.ssh/config .     // Edit config file

The config file should look like this

`# This is a comment 
''# Personal github account  
Host github.com  
   HostName github.com  
   User git  
   IdentityFile ~/.ssh/id_rsa_github# Personal gitlab account  
Host gitlab.com  
   HostName gitlab.com  
   User bgit  
   IdentityFile ~/.ssh/id_rsa_gitlab`==``==