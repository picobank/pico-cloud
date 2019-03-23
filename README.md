# Picobank RaspberryPI cluster experiment

## Setup

Downloads the latest Hypriot image:

    wget https://github.com/hypriot/image-builder-rpi/releases/download/v1.10.0/hypriotos-rpi-v1.10.0.img.zip

Install Hypriot's `flash` tool:

    curl -LO https://github.com/hypriot/flash/releases/download/2.3.0/flash
    chmod +x flash
    sudo mv flash /usr/local/bin/flash


Define your WIFI SSID and password in the user-data files:

    WIFI_SSID=MYSSID
    WIFI_PASSWORD=MYPASSWORD
    sed -i "" "s/ssid=\"[^\"]*\"/ssid=\"$WIFI_SSID\"/ ; s/psk=\"[^\"]*\"/psk=\"$WIFI_PASSWORD\"/" *.yaml

Optionally add your public RSA/DSA SSH keys to the user-data files:

    for i in *.yaml
    do
        (
            echo "ssh_authorized_keys:"
            for k in ~/.ssh/id_[rd]sa.pub
            do
                echo "  - $(cat "$k")"
            done
        ) >> $i
    done


Flash the various SD cards:

    sudo flash --userdata picobank-master.yaml -f -d /dev/sde hypriotos-rpi-v1.10.0.img.zip
