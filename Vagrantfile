VAGRANTFILE_API_VERSION = "2"

DEVELOP_IP = "192.168.33.10"
CI_IP      = "192.168.33.100"
DEPLOY_IP  = "192.168.33.200"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|

  if Vagrant.has_plugin?("vagrant-cachier")
    config.cache.scope = :box
  end

  config.vm.box = "centos/7"

  # 開発用仮想環境
  config.vm.define :develop do |develop|
    develop.vm.hostname = "develop"
    develop.vm.network :private_network, ip: DEVELOP_IP

    develop.vm.synced_folder "src", "/srv/httpd/src/current",
      id: "vagrant-root", :nfs => false,
      owner: "vagrant",
      group: "vagrant",
      :mount_options => ["dmode=775", "fmode=775"]

    #develop.vm.provision "ansible" do |ansible|
    #  ansible.playbook = "ansible/playbook.yml"
    #  ansible.sudo = true
    #  #ansible.inventory_path = "playbooks"
    #end

    develop.vm.provision :shell, inline: "echo Good job, now enjoy your new vbox: http://#{DEVELOP_IP}"
  end

  # CI環境
  config.vm.define :ci do |ci|
    ci.vm.hostname = "ci"
    ci.vm.network :private_network, ip: CI_IP
  end

  # デプロイ環境
  config.vm.define :deploy do |deploy|
    deploy.vm.hostname = "deploy"
    deploy.vm.network :private_network, ip: DEPLOY_IP
  end

end
