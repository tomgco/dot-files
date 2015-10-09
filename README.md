```sh
cd ~

if [ -z "${HOME}" ]; then
  HOME=${1:-/home/tomgco}
fi

echo "Dropping into root shell.";
sudo add-apt-repository -y ppa:pi-rho/dev
sudo apt-get update
sudo apt-get -y install git zsh vim tmux build-essential cmake python-dev trash-cli curl
sudo apt-get -y install {h,io,if}top  
sudo locale-gen en_GB.UTF-8

# Gives my shell a theme of nice-ness
git clone https://github.com/chriskempson/base16-shell.git ~/.config/base16-shell

#if [ -z "{$KEYED}" ]; then
#  sudo apt-get -y install gnupg2
#fi

git clone https://github.com/tomgco/dot-files.git
cd dot-files;
git submodule sync
git submodule update --init --recursive;
cd -;

# Create a symlink to all dot files in dot-files repo
ls -A dot-files/ | xargs -L 1 echo | grep -v '.git$' | xargs -L1 sh -c 'ln -s dot-files/$0 .'
# Change shell to zsh from bash
chsh -s /bin/zsh

# Installing Node version manager.
mkdir ~/.nave
cd ~/.nave
curl -LO http://github.com/isaacs/nave/raw/master/nave.sh
chmod +x nave.sh
sudo ln -s $PWD/nave.sh /usr/local/bin/nave
sudo nave usemain stable

# Compile YCM for vim autocomplete
cd ~/.vim/bundle/YouCompleteMe
./install.sh --clang-completer

# Linking Deps from dropbox
echo 'Skipping...';

cd -;
```
