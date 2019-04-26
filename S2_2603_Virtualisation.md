# La Virtualisation

| Machine hôte    | Système Hôte        |  
| ------------- |:-------------:|  
| La machine hôte représente la machine pyhisique qui va "héberger" un ou plusieurs VM.     | Il représente l'OS qui est installé sur la machine de base. |  

| Machine invité      | Système Invité      |
| ------------- |:-------------:|
| Elle représente la machine virtualisée créée et gérée par l'hyperviseur Virtual Box. On l'appelle aussi Client.  | Il représente l'OS installé sur la VM. |

## [VirtualBox](https://www.virtualbox.org/)
*logiciel libre de virtualisation publié par Oracle*  

## [Vagrant](https://www.vagrantup.com/)

**les commandes :**
* vagrant init : initialisation de vagrant, création du fichier "VagrantFile"
* vagrant up : lancement de la VM
* vagrant ssh : Ouverture du terminal sur la VM
* vagrant halt : couper la VM
* vagrant global-status : listing des VM sur la machine et leur disponibilité

**dans le fichier Vagrantfile**

 \# -*- mode: ruby -*-  
 \# vi: set ft=ruby :  

Vagrant.configure("2") do |config|  
  config.vm.box = "ubuntu/xenial64"  
  config.vm.network "private_network", ip: "192.168.33.77"  
  config.vm.synced_folder "./data", "/var/www/html/"  
  config.vm.provider "virtualbox" do |v|  
    v.name = "Fondue"  
  end  
end  

**Pour appliquer une modification, lancer "vagrant upload" une fois les modifications enregistrées**


**Créer un script pour lancer une VM la setup, et y installer apache2**  
\#!/bin/bash  
clear  
rm Vagrantfile  
rm -rf data/  
mkdir "data"  

touch "Vagrantfile"  
while [[ $inputos = '' ]]; do  
clear  
echo "Quel OS tu veux utiliser ?"  
read inputos  
done  
while [[ $inputip = '' ]]; do  
clear  
echo "Quelle sera l'ip de la VM ?"  
read inputip  
done  
while [[ $inputname = '' ]]; do  
clear  
echo "Comment tu veux appeler ta machine ?"  
read inputname  
done  
clear  
echo Gloire à $inputname  
echo Qui tournera sous $inputos  
echo A l\'adresse $inputip  

echo "\# -\*- mode: ruby -\*-  
\# vi: set ft=ruby :  
Vagrant.configure(\"2\") do |config|    
  config.vm.box = \"$inputos\"  
  config.vm.network \"private_network\", ip: \"$inputip\"  
  config.vm.synced_folder \"./data\", \"/var/www/html/\"  
  config.vm.provider \"virtualbox\" do |v|  
    v.name = \"$inputname\"  
   end  
end" >> Vagrantfile  

echo '\#!/bin/bash  
sudo apt-get update  
sudo apt-get install -y apache2' >> ./data/scriptApache2.sh  

vagrant up  
vagrant ssh  

*lancer bash /var/www/html/scriptApache2 sur le terminal de la VM*
