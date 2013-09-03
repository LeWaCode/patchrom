Patchrom
===========

Get Android SDK
----------------

In order to build LeWa patchrom, you should have the [android sdk installed](https://developer.android.com/sdk/installing.html).

Then add sdk tools and platfrom tools to PATH

$ vim .bashrc

export PATH=$PATH:~/android-sdk/tools:~/android-sdk/platform-tools

Getting Started
---------------

To get started with LeWaCode/patchrom, you'll need to get familiar with [Git and Repo](http://source.android.com/source/using-repo.html).

To initialize your local repository using the LeWa patchrom trees, use a command like this:

    mkdir patchrom

    cd patchrom

    repo init -u git://github.com/LeWaCode/patchrom.git -b jellybean

Then to sync up:

    repo sync

Build
--------

Assumed current directory is patchrom and you want to build the ROM for Xiaomi m1s


    . build/envsetup.sh

    cd m1s

    make fullota

After build completed, there will be a fullota.zip under out directory, now you can flash this file into your device.

Porting device
----------------

Asssumed current directory is patchrom and you want to port lewa to a new android device maguro

Prerequiste:

(1) Your device has root or has a rooted kernel

(2) Your device has CWM or TWRP recovery

Workflow:

(1) Connect your device to PC, ensure adb works

(2) Run the following commonds in terminal

    . build/envsetup.sh

    mkdir maguro

    cd maguro

    adb reboot recovery

    ../tools/releasetools/ota_target_from_phone -r (this will generate a stockrom.zip, flash this zip in recovery mode to ensure it works)

    cp ../build/makefile . (change the local-zip-files to stockrom.zip, read the comments in makefile)

    make workspace

    make firstpatch (this command will patch the lewa code into framework.jar, services.jar and android.policy.jar, you should resolve the conflict in temp/reject)

    make fullota

Now you get the LEWA ROM that you port for maguro, enjoy it!



