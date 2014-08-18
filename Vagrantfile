# -*- mode: ruby -*-
# vi: set ft=ruby :

# This Vagrantfile needs Docker provider support
Vagrant.require_version ">= 1.6.3"

ROOT = File.dirname(File.absolute_path(__FILE__))

# Default env properties which can be overridden
DOCKERHOST_VAGRANT_PATH = ENV['DOCKERHOST_VAGRANT_PATH'] || '../..'

# Machine-specific properties
RAILO_FWDPORT_HTTP = ENV['RAILO_FWDPORT_HTTP'] || '48080'
RAILO_FWDPORT_AJP = ENV['RAILO_FWDPORT_AJP'] || '48081'

# Vagrantfile API/syntax version. Don't touch unless you know what you're doing!
VAGRANTFILE_API_VERSION = '2'

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|

  # Common Docker machine settings
  dockerhost_vagrant_path = File.absolute_path(DOCKERHOST_VAGRANT_PATH, ROOT)
  config.vm.synced_folder ".", "/vagrant", :disabled => true
  config.ssh.username = 'root'
  
  # Docker machines
  
  config.vm.define "railo", autostart: true do |m| 
    m.vm.provider :docker do |d|
      d.build_dir           = "./railo"
      d.ports               = ["#{RAILO_FWDPORT_HTTP}:8888,#{RAILO_FWDPORT_AJP}:8009"]
      d.cmd                 = ['/sbin/my_init','--enable-insecure-key']
      d.has_ssh             = true
      d.vagrant_vagrantfile = File.join(dockerhost_vagrant_path,'Vagrantfile')
    end
  end

end
