# ZorinDriver04f3-0c00
Fingerprint driver for HP Probook 470 G8 Elan 04f2:0c00

Installation Instructions for Custom libfprint Files

Download and extract the archive:
Place custom-libfprint.tar.gz in your home directory and run:

tar xzvf custom-libfprint.tar.gz

This will extract the files into the current directory.

Backup your existing files (optional but recommended):
Before replacing any files, backup your existing libfprint library and module. For example:

sudo cp /usr/lib/x86_64-linux-gnu/libfprint-2.so.2 /usr/lib/x86_64-linux-gnu/libfprint-2.so.2.backup
sudo cp /usr/lib/x86_64-linux-gnu/libfprint-2/libfprint-2-tod.so.* ~/backup/
Install the new files:

For the main library:
Copy libfprint-2.so.2.0.0 to the appropriate directory:

sudo cp libfprint-2.so.2.0.0 /usr/lib/x86_64-linux-gnu/
Then update (or recreate) the symlink so that the system uses the new version:

cd /usr/lib/x86_64-linux-gnu/
sudo ln -sf libfprint-2.so.2.0.0 libfprint-2.so.2
sudo ln -sf libfprint-2.so.2.0.0 libfprint-2.so
For the custom driver module:
Copy libfprint-2-tod.so.1 to the libfprint module directory:

sudo cp libfprint-2-tod.so.1 /usr/lib/x86_64-linux-gnu/libfprint-2/
Set the correct permissions:
Ensure both files are readable by all users:

sudo chmod 644 /usr/lib/x86_64-linux-gnu/libfprint-2.so.2.0.0
sudo chmod 644 /usr/lib/x86_64-linux-gnu/libfprint-2/libfprint-2-tod.so.1
Update the dynamic linker cache:
Run:

sudo ldconfig
Restart the fingerprint service:
Restart fprintd so it picks up the new files:

sudo systemctl restart fprintd
Test the fingerprint sensor:
Try enrolling your fingerprint:

fprintd-enroll
If the sensor is now detected, you should be able to enroll your fingerprint successfully.

