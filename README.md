

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

sudo umount /dev/mmcblk0p1 /dev/mmcblk0p2
rmdir tmpboot tmproot

Install the SD Card in your Raspberry Pi and boot. Wait for the boot process to finish (wait 5 minutes for activity lights to stop flashing)
sudo rfkill unblock 0

# next check if networking over wifi is working
ifconfig wlan0
ssh pi@raspberrypi.local


sudo apt update
sudo apt-get install libhdf5-dev libhdf5-serial-dev libhdf5-103 libqtgui4 libqtwebkit4 libqt4-test python3-pyqt5 libatlas-base-dev libjasper-dev
sudo apt-get install build-essential cmake pkg-config libjpeg-dev libtiff5-dev libjasper-dev libpng-dev
sudo apt-get install libavcodec-dev libavformat-dev libswscale-dev libv4l-dev  libxvidcore-dev libx264-dev libfontconfig1-dev libcairo2-dev libgdk-pixbuf2.0-dev libpango1.0-dev libgtk2.0-dev libgtk-3-dev gfortran
sudo apt-get install python3-dev
sudo apt install libzmq-dev python3-zmq

wget https://bootstrap.pypa.io/get-pip.py
sudo python3 ./get-pip.py
export ARCHFLAGS="-mcpu=cortex-a72 -mfloat-abi=hard -mfpu=neon-fp-armv8 -funsafe-math-optimizations -fomit-frame-pointer -ftree-vectorize"
pip install "picamera[array]" --user
pip install imutils --user
pip install imagezmq --user
pip install opencv-python==4.4.0.46 --user

# download the pre-compiled mxnet/openblas installer and run it
TODO: extract to .local and /opt and update .bashrc



