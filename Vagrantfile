# -*- mode: ruby -*-
# vi: set ft=ruby :

# Variables
## Infrastructure
$box_image = "ubuntu/xenial64"

## XVM folder and file names
$xvm_folder = "./xvm"
$xvm_jar = "xvm-1.0.jar"

## XVM port
$xvm_port = 8080

## Scripts
$build_prereq = <<SCRIPT
echo "...Updating OS..."
apt-get update -y && apt-get upgrade -y
echo "...Installing JAVA 1.8..."
apt-get install openjdk-8-jre -y
SCRIPT


$create_xvm_service = <<SCRIPT
echo "...Create XVM systemd service file..."
cat > xvm.service <<EOF
[Unit]
Description=XVM
Documentation=https://labs.vmware.com/flings/cross-vcenter-workload-migration-utility#summary

[Service]
WorkingDirectory=/home/ubuntu/xvm
ExecStart=/bin/bash -c "java -jar /home/ubuntu/xvm/#{$xvm_jar}"
User=ubuntu 

Restart=on-failure
RestartSec=5

[Install]
WantedBy=multi-user.target
EOF

mv xvm.service /etc/systemd/system/

echo "...Create service and start it..."
systemctl daemon-reload
systemctl enable xvm
systemctl start xvm

SCRIPT

Vagrant.configure("2") do |config|

    config.vm.box = $box_image

    config.vm.network "forwarded_port", :guest => 8080, :host => $xvm_port

    config.vm.provision "file", source: $xvm_folder, destination: "$HOME/$xvm_folder"
    
    config.vm.provision "shell", inline: <<-SHELL
        #{$build_prereq}
        #{$create_xvm_service}
    SHELL
end    
