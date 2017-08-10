Vagrant.configure("2") do |config|

  config.ssh.insert_key = false

  if Vagrant.has_plugin?("vagrant-vbguest") then
    # Guest Additions自動更新の無効化設定
    config.vbguest.auto_update = false
  end

  config.vm.box = "CentOS7.0"

  # 共有フォルダの設定
  config.vm.synced_folder "./manage", "/www/marr_manage",  create: true, owner: "vagrant", group: "vagrant"

  # Every Vagrant development environment requires a box. You can search for
  # boxes at https://atlas.hashicorp.com/search.
  config.vm.define "ansible" do |server|
    server.vm.hostname = "ansilble1"
    server.vm.network :private_network, ip: "192.168.33.35"

    # VirtualBoxのGUI上の名前を設定する
    server.vm.provider "virtualbox" do |vb|
      vb.name = config.vm.box.gsub(/\//, "_") + "_" + server.vm.hostname
    end

    server.vm.provision "ansible_local" do |ansible|
      ansible.playbook = "playbook.yml"
    end

  end
end
