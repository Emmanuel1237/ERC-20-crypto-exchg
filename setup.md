#### If you are using a Linux/mac OS then Start from Step 1 onwards.

#### If you are using windows then I recommend setting up Windows Subsystem for Linux (WSL) . follow Steps A to C and then continue from Step 1 onwards.

## WSL SETUP FOR DAPP DEVELOPMENT ( UBUNTU WSL )
### step A
Before installing any Linux distros for WSL, you must ensure that the "Windows Subsystem for Linux" optional feature is enabled:

=> Open PowerShell as Administrator and run:

     Enable-WindowsOptionalFeature -Online -FeatureName Microsoft-Windows-Subsystem-Linux

=>Restart your computer when prompted.

### step B
=> install Ubuntu from windows store ( approx ~260 mb ).

The first time you launch a Linux distribution in Windows, you will be prompted to create a UNIX username and password.

=> Update the Linux distribution.

After you have set up your user, update the OS.

To do this run:

     sudo apt-get update && sudo apt-get upgrade -y && sudo apt-get upgrade -y && sudo apt-get dist-upgrade -y && sudo apt-get autoremove -y

### step C
=> Graphical Applications
In order to run Linux GUI applications using WSL, you must:

    1. Install a X server for Windows
    2. Configure bash to tell GUIs to use the local X server

#### Install VcXsrv
In order to run graphical Linux applications, you’ll need an X server.

[VcXsrv](https://sourceforge.net/projects/vcxsrv/) is the only fully open source and up-do-date native X server for Windows. Download and run the latest installer, then locate the XLaunch shortcut in the Start Menu, and click it.

You will be greeted with a setup wizard. Accept the default options. On the last page of the wizard, click on the Save configuration button, and save the configuration file in %appdata%\Microsoft\Windows\Start Menu\Programs\Startup, so vcXsrv will launch at startup without asking about these options, then click on the Finish button.

A X icon will appear in your system tray.

#### Configure bash to use the local X server
In bash run:
 
    1. echo "export DISPLAY=localhost:0.0" >> ~/.bashrc
    2. To have the configuration changes take effect, restart bash, or run:
      ~/.bashrc

#### Test a graphical application
Install x11-apps
   
    sudo apt-get install x11-apps
    Run: xeyes

A new window will open, containing a pair of eyes that will follow your mouse movements.

#### Congrats! you have successfully setup your WSL.Now continue from step 1.

## Mac/Linux users begin from here onwards.
### step 1 
=> Now let us install an text editor 

#### Installing Sublime Text on Ubuntu in WSL
To install Sublime Text 3 on your Ubuntu WSL, follow these steps:

#### Update the apt package list and install the dependencies necessary to fetch packages from https sources:

    sudo apt update
    sudo apt install apt-transport-https ca-certificates curl software-properties-common

#### Import the repository’s GPG key using the following curl command:

    curl -fsSL https://download.sublimetext.com/sublimehq-pub.gpg | sudo apt-key add -

#### Add the Sublime Text APT repository to your system’s software repository list by typing:

    sudo add-apt-repository "deb https://download.sublimetext.com/ apt/stable/"

#### Once the repository is enabled, update apt sources and install Sublime Text 3 with the following commands:

    sudo apt update
    sudo apt install sublime-text

That’s it. Sublime Text has been installed on your Ubuntu WSL.

Starting Sublime Text
  You can start the Sublime Text editor from the terminal by typing subl.

### step 2

=> we need to install the Ethereum package for our sublime text editor
#### Package Control in Sublime Text, Setting up for Solidity Development(For syntax highlighting)

1. For Sublime Text 3  , View> Show Console  Paste the following and hit ENTER
    
    import urllib.request,os,hashlib; h = '6f4c264a24d933ce70df5dedcf1dcaee' + 'ebe013ee18cced0ef93d5f746d80ef60'; pf = 'Package Control.sublime-package'; ipp = sublime.installed_packages_path(); urllib.request.install_opener( urllib.request.build_opener( urllib.request.ProxyHandler()) ); by = urllib.request.urlopen( 'http://packagecontrol.io/' + pf.replace(' ', '%20')).read(); dh = hashlib.sha256(by).hexdigest(); print('Error validating download (got %s instead of %s), please try manual install' % (dh, h)) if dh != h else open(os.path.join( ipp, pf), 'wb' ).write(by)

2. Restart Sublime Text
3. CTRL , SHIFT , P > Should launch the package control window.
4. Type Install ….Select Install Package
5. Type Ethereum and install both Ethereum and EthereumSoliditySnippets

That’s it  now, when you create a .sol file in Sublime Text, you should see styling, syntax highlighting and most importantly, intellisense.

### step 3

=> Now let us install some dependencies required.
#### Install and Configure brew (just to install npm using homebrew)

Run the following to install brew as Linuxbrew.
   
    sh -c "$(curl -fsSL https://raw.githubusercontent.com/Linuxbrew/install/master/install.sh)"

(Pay close attention to the output; you’ll be instructed to Configure Linuxbrew in your ~.profile and Add Linuxbrew to your PATH. Normally, Homebrew on MacOS will install packages to /usr/local/bin or /usr/local/Cellar. Linuxbrew, on the other hand, will install packages to /home/linuxbrew/.linuxbrew/bin. Therefore, you will need to manually add that directory to your PATH. Additionally, this means that you won’t need to use sudo to usebrew.)

Run these commands:

    test -d ~/.linuxbrew && eval $(~/.linuxbrew/bin/brew shellenv)

    test -d /home/linuxbrew/.linuxbrew && eval $(/home/linuxbrew/.linuxbrew/bin/brew shellenv)

    test -r ~/.bash_profile && echo "eval \$($(brew --prefix)/bin/brew shellenv)" >>~/.bash_profile

    echo "eval \$($(brew --prefix)/bin/brew shellenv)" >>~/.profile

And that’s it! Now you can use brew! Try installing a simple package to test:

    brew install hello
    Run: hello

You should get the  output as "Hello, world!" if everything is working as expected. If you get an error concerning 'patchelf', see below for a fix. 

#### Error: patchelf fix
 If you have the following error:
    Error: patchelf must be installed: brew install patchelf
    Warning: Bottle installation failed: building from source.
    Error: The following formula
    patchelf
    cannot be installed as binary package and must be built from source.

The recommended solution of brew install gcc may result in the same error. A fix is to run the following commands to get brew working properly.

    sudo apt-get update
    sudo apt-get install build-essential

Now test again, it should be working..

### step 4
=> Ok, now lets install our first dependency ie. NPM ( Node Package Manager ) it comes bundeled with node js.

#### To install 
    Run: brew install node
#### TO confirm installation
    Run: node -v 

=> since for this project we need node version 9.10.0 so follow bellow steps for installing it.

=> Another way to install Node.js and NPM is with the Node Version Manager (NVM). NVM is a tool practical for managing multiple Node.js versions.

  1. To install NVM, download the installation script from GitHub. For that, you will use the curl command line.
  If you do not have curl, install it by running:

    sudo apt install curl
  Press y to confirm the installation and hit Enter.

  2. Now, download the NVM installation script with the command:

    curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.33.11/install.sh | bash
  It automatically clones the NVM repository and adds the NVM path to ZSH or Bash.

  3. To enable nvm:

    Close and open the terminal or
    Run the given command

  4. Finally, check whether the installation was successful by verifying nvm version:

    nvm --version

  Once you have installed nvm, you can find a list of all the available Node.js versions with the command:

    nvm ls-remote

This will list all available versions of nvm, including the latest LTS version.

Note: LTS stands for long-term support and is used for software that is maintained for an  extended period and is recommended as being the most stable.

#### Install a Specific Version
Nvm is a package manager; it can install and manage multiple Node.js versions.

To install a particular version, use the command: nvm install and add the number of the version.

For example for: nvm install 9.10.0

To view all installed versions on your manager, use the command:

    nvm ls

This will list all installed Node.js versions as well as the default and stable versions.

=> list installed nodejs versions
To check which version you are currently using, run the command:

    node -v 

To switch versions of Node.js (if you have already installed it on the NVM) enter the command:

    nvm use 9.10.0

### step 5
=> Now lets install our next dependency ie the Truffle framework it allows us to create decentralized apps in the ethereum network,also gives us a framework for testing our smart contracts,it gives us a set of tools to deploy our smartcontracts to the blockchain. We can also develop our client side application using Truffle.

Truffle is a development environment, testing framework and asset pipeline for Ethereum, aiming to make life as an Ethereum developer easier. With Truffle, you get:

  - Built-in smart contract compilation, linking, deployment and binary management.
  - Automated contract testing with Mocha and Chai.
  - Configurable build pipeline with support for custom build processes.
  - Scriptable deployment & migrations framework.
  - Network management for deploying to many public & private networks.
  - Interactive console for direct contract communication.
  - Instant rebuilding of assets during development.
  - External script runner that executes scripts within a Truffle environment.

#### For this project use truffle version 5.1.14
     Run: npm install --g truffle@5.1.14

=>For normal truffle installations(not needed for this project)
#### To install
    Run: npm install -g truffle
#### To confirm installation
    Run: truffle -v

### step 6
=>now lets install our next dependency ie. ganache, it is a local inmemory blockchain that we will use for development purposes.

#### To install

Visit truffle web site [here](https://www.trufflesuite.com/ganache)
select your OS and download Ganache.

### step 7 
=> Next dependency is the metamask extension for chrome, in order to use the blockchain we must connect to it (remember blockchain is a network) we have to install a special browser extension in order to use Ethereum blockchain, that's where metamask comes in. We willl be able to connect to our local ethereum network with our personal account and interact with the smart contract using metamask

#### To install
Go to [here](https://metamask.io/) ,download and enable metamask extension on chrome.