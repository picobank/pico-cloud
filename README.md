# Picobank RaspberryPI cluster experiment

## Setup

Downloads the latest Hypriot image:

    wget https://github.com/hypriot/image-builder-rpi/releases/download/v1.10.0/hypriotos-rpi-v1.10.0.img.zip

Install Hypriot's `flash` tool:

    curl -LO https://github.com/hypriot/flash/releases/download/2.3.0/flash
    chmod +x flash
    sudo mv flash /usr/local/bin/flash

Flash the various SD cards:

    sudo flash --userdata picobank-master.yaml -f -d /dev/sde hypriotos-rpi-v1.10.0.img.zip
