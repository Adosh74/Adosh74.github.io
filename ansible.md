# Ansible

- [Ansible](#ansible)
- [My Ansible File](#my-ansible-file)
- [Tools](#tools)
- [How use it](#how-use-it)

I use  `ansible` to install the necessary tools I need in development when using a new machine to start quickly. I have a playbook that installs all the tools I need.

# My Ansible File

```yaml
- hosts: localhost
  become: true
  pre_tasks: 
    - name: Update cache
      apt:
        update_cache: true
      tags:
      - zsh
      - nodejs
      - tmux
  tasks: 
  - name: Install zsh
    apt: name=zsh
    tags: 
    - zsh
  - name: Change shell
    shell: chsh -s `which zsh`
    tags:
    - zsh
  - name: Install ohmyzsh (:XD)
    shell: curl -L https://raw.github.com/robbyrussell/oh-my-zsh/master/tools/install.sh | sh
    tags:
    - zsh
  - name: Install the zsh plugins for auto suggestions
    shell: git clone https://github.com/zsh-users/zsh-autosuggestions.git ~/.oh-my-zsh/plugins/zsh-autosuggestions
    tags:
    - zsh
  - name: Update our zshrc
    shell: sed -i -e 's/plugins=(git)/plugins=(git zsh-autosuggestions)/g' ~/.zshrc
    tags:
    - zsh
  - name: Install tmux
    apt:  name=tmux
    tags:
    - tmux
  - name: Install nvm
    shell: >
     curl https://raw.githubusercontent.com/creationix/nvm/v0.7.0/install.sh | sh
     creates=/home/{{ ansible_user_id }}/.nvm/nvm.sh
    tags:
    - nodejs
  - name: Install node latest version
    shell: >
      /bin/bash -c "source ~/.nvm/nvm.sh && nvm install node"
      creates=/home/{{ ansible_user_id }}/.nvm/alias
    tags:
    - nodejs
  - name: Install node version 20.10
    shell: >
     /bin/bash -c "source ~/.nvm/nvm.sh && nvm install 20.10"
     creates=/home/{{ ansible_user_id }}/.nvm/alias
    tags:
    - nodejs
```

# Tools

- zsh
- zsh autosuggestions
- oh-my-zsh
- tmux
- nvm
- nodejs latest version
- nodejs version 20.10

# How use it

1. Install ansible
2. Clone the repository

 ```bash
    git clone https://github.com/Adosh74/ansible
 ```

3. move to the directory

 ```bash
    cd ansible
 ```

4. Run the playbook

 ```bash
    ansible-playbook local.yml
 ```
