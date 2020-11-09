#####
 wex
#####

**wex** is a shell script which configures external USB camera as a webcamera
or for video recording on a Linux system. The script was tested on Fedora 31, 32 and 33.

==============
 Installation
==============

Before you run the script first time, check that following packages are installed on your system::

        ffmpeg
        gphoto2
        v4l2loopback

``v4l2loopback``, which source code is available at `GitHub <https://github.com/umlaeute/v4l2loopback>`_, is not a standard part of Fedora distribution. It can be installed from `Fedora COPR repository 
<https://copr.fedorainfracloud.org/coprs/sentry/v4l2loopback/>`_::

        $ dnf copr enable sentry/v4l2loopback
        $ dnf install v4l2loopback

=======
 Usage
=======

The script runs with various parameters::

        wex [-h|--help] [-a|--activate] [-c|--camera <name>] [-d|--device <number>] [-i|--info] [-r|--remove]

The parameters mean::

        -h, --help              display help message
        -a, --activate          activate external USB camera using v4l2loopback device
        -c, --camera <name>     external camera name
        -d, --device <number>   video device number
        -i, --info              video devices and external USB camera information
        -r, --reset             reset v4l2loopback devices

The script uses restricted commands which need administrative rights. Therefore, such commands are run with ``sudo``,
and the user is prompted for their password.

============
 Experience
============

The script has been developed to cofigure the external camera for videoconferencing (BlueJeans, Google Meet).
Video live streaming can be checked with `Open Broadcaster Software (OSB) <https://obsproject.com/>`_.
There is possible to select an internal or external camera.

The script is prepared for a connection of ``Canon EOS 6d Mark II`` DSLR camera via USB 2.0.

There is assigned ``/dev/video10`` device by default.
The assigned device is labeled with the camera name to make the device identification easier.

You can modify both values either by ``--camera`` and/or ``--device`` parameters
or by changing ``CAMERA`` and/or ``DEVICE`` variables in the script. If the video device has already been set
and should be changed, reset v4l2loopback devices by running wex with ``--reset`` parameter.

=============
 Limitations
=============

USB 2.0 throughput limits the resolution to 1024x576px and 25fps on Canon EOS 6D Mark II camera.

The script supports neither cameras connected with HDMI cable directly nor 
through HDMI to USB convertors which would enable Full HD 1080p resolution on USB 3.0 interface.

The script was tested with only one external connected camera.
