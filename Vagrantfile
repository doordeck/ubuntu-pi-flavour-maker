# -*- mode: ruby -*-
# vi: set ft=ruby :

########################################################################
#
# Copyright (C) 2016 Michael Barnwell <michael@doordeck.com>
#
# This program is free software; you can redistribute it and/or
# modify it under the terms of the GNU General Public License
# as published by the Free Software Foundation; either version 2
# of the License, or (at your option) any later version.
#
# This program is distributed in the hope that it will be useful,
# but WITHOUT ANY WARRANTY; without even the implied warranty of
# MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
# GNU General Public License for more details.
#
# You should have received a copy of the GNU General Public License
# along with this program; if not, write to the Free Software
# Foundation, Inc., 51 Franklin Street, Fifth Floor, Boston, MA  02110-1301, USA.
########################################################################

# Required to fix SSH identity issue with ansible
Vagrant.require_version ">= 1.7.4"

Vagrant.configure(2) do |config|
  config.vm.box = "ubuntu/xenial64"
  config.vm.synced_folder ".", "/vagrant", disabled: false

  config.vm.define "build"

  config.vm.provider "virtualbox" do |vb|
    vb.name = "build-vm"
  end

  $script = <<SCRIPT
    cd /vagrant && /vagrant/build-image.sh
    sudo rsync --progress /root/PiFlavourMaker/xenial/ubuntu-minimal-16.04.2-server-armhf-raspberry-pi.img /vagrant/
SCRIPT

  config.vm.provision "shell", privileged: true, inline: $script

end

