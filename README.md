# face-recognition
install libraries for face-recognition on raspberry pi, preferrably a Raspi 4, but all can be used.

Here are the steps to install the face recognition library on your Raspberry Pi. I recommend using a Raspberry Pi 4 for better responsiveness, but this process should work on other models as well.

Update and Upgrade: Open a terminal on your Raspberry Pi and run the following commands one at a time:
sudo apt-get update
sudo apt-get upgrade

Install Dependencies: Install the necessary dependencies with the following commands:
sudo apt-get install build-essential cmake gfortran git wget curl graphicsmagick libgraphicsmagick1-dev libatlas-base-dev libavcodec-dev libavformat-dev libboost-all-dev libgtk2.0-dev libjpeg-dev liblapack-dev libswscale-dev pkg-config python3-dev python3-numpy python3-pip zip

Increase the SWAP FILE: Edit the swap file configuration:
sudo nano /etc/dphys-swapfile
Change CONF_SWAPSIZE=100 to CONF_SWAPSIZE=1024, save, and exit. Then restart the swap service:
sudo /etc/init.d/dphys-swapfile

Git Clone and Install dlib Library: Clone the dlib repository and install it:
mkdir -p dlib
git clone -b 'v19.6' --single-branch https://github.com/davisking/dlib.git dlib/
cd ./dlib
mkdir build; cd build
cmake ..
cmake --build .
pip3 install dlib

Decrease the SWAP Size: Edit the swap file configuration again:
sudo nano /etc/dphys-swapfile
Change CONF_SWAPSIZE=1024 back to CONF_SWAPSIZE=100, save, and exit. If this step fails, follow the same process as in Step 3.
Install Supporting Libraries: Install additional libraries required for dlib and face_recognition:
pip3 install numpy scikit-image
sudo apt-get install python3-scipy libjasper-dev libqtgui4 python3-pyqt5 libqt4-test
pip3 install opencv-python==3.4.6.27
pip3 install face_recognition

Clone the Face Recognition Library: Clone the face_recognition repository and try out some examples:
git clone --single-branch https://github.com/ageitgey/face_recognition.git
cd ./face_recognition/examples
python3 facerec_on_raspberry_pi.py

All done!
