1. Make sure your machine is fully up-to-date with any OS X updates.
2. Enable full disk encryption via FileVault:
`System Preferences > Security & Privacy > FileVault > Turn On FileVault...`
3. Generate an SSH keypair:
`ssh-keygen -t rsa` (select all defaults)
4. Add your SSH key to your Github user and then check that it works:
`ssh -T git@github.com`
5. Install [Homebrew](https://brew.sh/).
6. Install base packages:
```
brew install git
brew install pyenv
brew install hdf5
brew install h5utils
brew install python3
```
7. Add Pyenv to your system path, by adding the following line to your `.bashrc` or `.bash_profile`:
`eval "$(pyenv init -)"`
8. Create your coding workspace:
`mkdir ~/osaro`
9. Clone Odin:
```
cd ~/osaro
git clone git@github.com:OsaroAI/odin.git odin
```
10. 