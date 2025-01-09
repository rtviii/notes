
# A process for setting up a new environemnet on a remote node.
(A docker container in the works)

<!-- Process -->
Copy dotfiles

```bash
# ------- zsh 
apt update && apt upgrade
apt install zsh

# ------- oh-my-zsh  (Make sure to source the correct path as ZSH in .zshrc)
sh -c "$(curl -fsSL https://raw.github.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"

# ------- plugins 
plugins=(
"https://github.com/ranger/ranger.git"
"https://github.com/zsh-users/zsh-syntax-highlighting"
"https://github.com/softmoth/zsh-vim-mode"
"https://github.com/zsh-users/zsh-autosuggestions"
"https://github.com/zsh-users/zsh-history-substring-search"
#...)
for plug in ${plugins[@]}; do git clone  $ZSH/plugins/$plug; done


# ------- nvim
sudo add-apt-repository ppa:neovim-ppa/unstable
sudo install neovim
git clone --depth 1 https://github.com/wbthomason/packer.nvim ~/.local/share/nvim/site/pack/packer/start/packer.nvim

# ------- Pull down configs
git clone https://github.com/rtviii/dotfiles

# ------- unpack configs

cp -r dotfiles/.config -> ~/
cp dotfiles/.zshrc -> ~/
cp dotfiles/.tmux.conf -> ~/

```
 
<!-- Dev -->

```bash


sudo apt install python3-venv python3-pip
python3 -m pip install --user virtualenv

```

<!-- Aux ideas -->
- would be nice to have tmux or terminal pick up the ip and display an icon or change color based on the host.



