Vagrant.configure("2") do |config|

  config.ssh.insert_key = false

  if Vagrant.has_plugin?("vagrant-vbguest") then
    # Guest Additions�����X�V�̖������ݒ�
    config.vbguest.auto_update = false
  end

  config.vm.box = "CentOS7.0"

  # ���L�t�H���_�̐ݒ�
  config.vm.synced_folder "./manage", "/www/marr_manage",  create: true, owner: "vagrant", group: "vagrant"

  # Every Vagrant development environment requires a box. You can search for
  # boxes at https://atlas.hashicorp.com/search.
  config.vm.define "ansible" do |server|
    server.vm.hostname = "ansilble1"
    server.vm.network :private_network, ip: "192.168.33.35"

    # VirtualBox��GUI��̖��O��ݒ肷��
    server.vm.provider "virtualbox" do |vb|
      vb.name = config.vm.box.gsub(/\//, "_") + "_" + server.vm.hostname
    end

    server.vm.provision "ansible_local" do |ansible|
      ansible.playbook = "playbook.yml"
    end

  end
end
