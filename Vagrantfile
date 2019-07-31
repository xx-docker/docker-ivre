ENV['VAGRANT_DEFAULT_PROVIDER'] = 'docker'
ENV['VAGRANT_CHECKPOINT_DISABLE'] = 'true'

VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|

  # Common options
  config.vm.synced_folder ".", "/vagrant", disabled: true

  # The DB server
  config.vm.define 'ivredb' do |db|
    db.vm.provider "docker" do |docker|
      docker.image = 'ivre/db'
      docker.name = 'ivredb'
    end
    db.vm.synced_folder "var_lib_mongodb", "/var/lib/mongodb"
    db.vm.synced_folder "var_log_mongodb", "/var/log/mongodb"
  end

  # The Web server
  config.vm.define 'ivreweb' do |web|
    web.vm.provider "docker" do |docker|
      docker.link('ivredb:ivredb')
      docker.image = 'ivre/web'
      docker.name = 'ivreweb'
    end
    web.vm.network "forwarded_port", guest: 80, host: 80
  end

  # The command line client
  config.vm.define 'ivreclient' do |client|
    client.vm.provider "docker" do |docker|
      docker.link('ivredb:ivredb')
      docker.image = 'ivre/client'
      docker.name = 'ivreclient'
      docker.create_args = ['-i', '-t']
    end
    client.vm.synced_folder "ivre-share", "/ivre-share"
  end

end