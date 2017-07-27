# Home-Assistant


## Update & Upgrade Raspberry Pi

``` bash
$ sudo apt-get update
$ sudo apt-get upgrade
$ sudo apt-get dist-upgrade
$ sudo apt-get autoremove
$ sudo apt-get autoclean
```

## Configure network access and enable SSH

**Enable SSH**

``` markdown
1. Enter `sudo raspi-config` in a terminal window
2. Select `Interfacing Options`
3. Navigate to and select `SSH`
4. Choose `Yes`
5. Select `Ok`
6. Choose `Finish`
```

**Find IP-Addreass**

``` markdown
1. Enter `hostname -I` in a terminal window
```

> Here you can see a device with hostname raspberrypi has IP address like this `192.168.0.115`

## Connect to RaspberryPi from PC

``` markdown
1. Enter `ssh pi@<pi ipadress>` -> `ssh pi@192.168.0.115` in a terminal window
2. If it want the authenticity of host. Type `yes` and press `Enter`
3. Enter raspberry pi password default `raspberry`
```

 ## Configure and Test the Audio

1. Find recording and playback devices.
    
    a. Note the card and device number for recording.
        
        $ arecord -l

    > **** List of CAPTURE Hardware Devices **** \
    > card 1: C920 [HD Pro Webcam C920], device 0: USB Audio [USB Audio]
    >> card number is 1, device number is 0

    b. Note the card and device number for playback.

        $ aplay -l

    > **** List of PLAYBACK Hardware Devices **** \
    > card 0: ALSA [bcm2835 ALSA], device 0: bcm2835 ALSA [bcm2835 ALSA] \
    > card 0: ALSA [bcm2835 ALSA], device 1: bcm2835 ALSA [bcm2835 IEC958/HDMI]
    >> card number is 0, device number is 0

2. Create a new file named `.asoundrc` in home directory `/home/pi`

    ``` bash
    pcm.!default {
        type asym
        capture.pcm "mic"
        playback.pcm "speaker"
    }
    pcm.mic {
        type plug
        slave {
            pcm "hw:<card number>,<device number>"
        }
    }
    pcm.speaker {
        type plug
        slave {
            pcm "hw:<card number>,<device number>"
        }
    }
    ```
3. Set 3.5mm jack speaker connected

    ``` markdown
    1. Enter `sudo raspi-config` in a terminal window
    2. Select `Advanced Options`
    3. Navigate to and select `Audio`
    4. Navigate to and select `Force 3.5mm ('headphone) jack`
    5. Choose `Finish`
    ```
4. Check that recording and playback work
    
    Play a test sound. Press `ctrl+c` when done.
    ```
    $ speaker-test -t wav
    ```

    Install SOX to record and playback
    ```
    $ sudo apt-get install -y sox
    ```
    Record audio clip. Press `ctrl+c` when done.
    ```
    $ rec t.wav
    ```
    Check the recording by replaying it.
    ```
    $ play t.wav
    ```
    
## Install

1. Update pip `sudo pip3 install -U pip setuptools`
2. Install VirtualENV `sudo pip3 install virtualenv`
3. Install packages

    ```
    sudo apt-get install -y portaudio19-dev
    ```

## Get-Started

1. Navigate to Documents directory. `cd Documents/`
2. Clone repository. `git clone https://github.com/SweiLz/home-assistant.git`
3. Navigate to repo directory. `cd home-assistant`
4. Setup python environments. `virtualenv -p python3 .env`
5. Begin virtual environment. `source .env/bin/active`
6. Install required packages. `pip3 install -r requirements.txt`