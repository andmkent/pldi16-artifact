# -*- mode: ruby -*-
# vi: set ft=ruby :

# Vagrantfile API/syntax version. Don't touch unless you know what you're doing!
VAGRANTFILE_API_VERSION = "2"

$script = <<SCRIPT

sudo apt-get update

# Install git, needed to clone our work
sudo apt-get install -y git

# Install libraries used by DrRacket
sudo apt-get install -y fontconfig libcairo2 libjpeg62 libpango1.0-0

# Install Racket 6.2.1

wget http://mirror.racket-lang.org/installers/6.2.1/racket-minimal-6.2.1-i386-linux-ubuntu-precise.sh
sh racket-minimal-6.2.1-i386-linux-ubuntu-precise.sh --dest ./racket-6.2.1
export PATH=$PATH:`pwd`/racket-6.2.1/bin/

# Check that Racket works
racket -v # print version

# Install our modified version of Typed Racket
raco pkg install --multi-clone convert --auto --clone typed-racket git://github.com/andmkent/typed-racket?path=typed-racket-lib#rtr-prototype

# Install our adapted version of the `math` library
raco pkg install --auto --clone math git://github.com/dkempe/math?path=math-lib
raco pkg install --auto --clone math git://github.com/dkempe/math?path=math-test

# Install our adapted version of the `plot` library
raco pkg install --auto --clone plot \
"git://github.com/andmkent/plot?path=plot-lib#rtr-prototype" \
"git://github.com/andmkent/plot?path=plot-compat#rtr-prototype" \
"git://github.com/andmkent/plot?path=plot-gui-lib#rtr-prototype" \
"git://github.com/andmkent/plot?path=plot-test#rtr-prototype"

# Install our adapted version of the `pict3d` library
raco pkg install --auto --clone pict3d \
"git://github.com/andmkent/pict3d?path=pict3d#rtr-prototype" \
"git://github.com/andmkent/pict3d?path=typed#rtr-prototype"

# Install DrRacket for trying examples
raco pkg install --auto drracket

# Clone our artifact repository for examples and Redex model
git clone git://github.com/andmkent/pldi16-artifact-misc

# Install full Racket 6.4 for using our Redex model 
# NOTE: This will NOT run our RTR examples!
wget http://mirror.racket-lang.org/installers/6.4/racket-6.4-i386-linux-ubuntu-precise.sh
sh racket-6.4-i386-linux-ubuntu-precise.sh --dest ./racket-6.4

SCRIPT

Vagrant.configure("2") do |config|
  config.vm.box = "hashicorp/precise32"
  config.vm.provision "shell",  inline: $script, :privileged => false
end