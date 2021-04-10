

sudo dd if=2020-02-13-raspbian-buster-lite.img of=/dev/mmcblk0 bs=4M
mkdir tmpboot tmproot
sudo mount /dev/mmcblk0p1 tmpboot
sudo mount /dev/mmcblk0p2 tmproot

touch tmpboot/ssh
echo "country=US
network={
    ssid="<YOUR_SSID>"
    psk="<YOUR_PSK>"
}
" | sudo tee -a tmproot/etc/wpa_supplicant/wpa_supplicant.conf
