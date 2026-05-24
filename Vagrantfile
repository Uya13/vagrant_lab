# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  # Используем образ CentOS 7 (Вариант 1)
  config.vm.box = "centos/7"

  # Цикл для создания двух машин (Вариант 0)
  (1..2).each do |i|
    config.vm.define "centos-vm-#{i}" do |node|
      # Задаем имя хоста внутри ВМ
      node.vm.hostname = "centos-vm-#{i}"

      # Настройка виртуальной сети, чтобы машины видели друг друга
      node.vm.network "public_network"

      # Конфигурация гипервизора VirtualBox
      node.vm.provider "virtualbox" do |vb|
        vb.memory = "1024" # 1 ГБ ОЗУ
        vb.cpus = 1
        vb.name = "PR4_CentOS_#{i}" # Имя машины в интерфейсе VirtualBox
      end

      # === ВАРИАНТ 0: Реализация общих папок (Метод VirtualBox) ===
      # Монтируем локальную папку ./shared в гостевую /home/vagrant/host_data
      node.vm.synced_folder "./shared", "/home/vagrant/host_data", type: "virtualbox"

      # === ВАРИАНТ 0: Провизия (File provisioner) ===
      # Копируем файл test.txt из локальной папки files в гостевую ОС
      node.vm.provision "file", source: "./files/test.txt", destination: "/home/vagrant/provisioned_file.txt"
    end
  end
end