# libuvc-theta-sample
Sample scripts for using the Ricoh Theta api and custom libuvc-theta to enable Ricoh Theta V/Z1 video livestreams to Linux via USB.

## Installation Guide
Main instructions taken from [https://codetricity.github.io/theta-linux/](https://codetricity.github.io/theta-linux/). 

1. Install libucv-theta
```
git clone https://github.com/ricohapi/libuvc-theta.git
sudo apt install libjpeg-dev
cd libuvc-theta
mkdir build
cd build
cmake ..
make
sudo make install
```

2. Install libucv-theta-samples
```
git clone https://github.com/ricohapi/libuvc-theta-sample.git
cd libuvc-theta-sample/gst
make
```

3. Install v4l2loopback for gst_loopback example.
```
git clone https://github.com/umlaeute/v4l2loopback.git
cd v4l2loopback
make
sudo make install
sudo depmod -a
sudo modprobe v4l2loopback
```

### Installation Problems
When installing v4l2loopbach I had to use sudo ie `sudo make && sudo make install`. I was attempting to build on Kinetic which has caused other people issues. If you encounter errors building v4l2loopback try this first.

## gst/gst_viewer
Decode and display sample using gstreamer. You may need gstreamer1.0 develpment packages to build and run.

## gst/gst_loopback
Feed decoded video to the v4l2loopback device so that v4l2-based application can use THETA video without modification.

CAUTION: gst_loopback may not run on all platforms, as decoder to v4l2loopback pipeline configuration is platform dependent

## Lines of note:
* Line 188: `pipe_proc = ....` - Defines the gstreamer elements for gst_loopback. Currently decodes the stream and directs it to v4l2sink to render video on /dev/video1
* Line 192: `pipe_proc = ....` - Defines the gstreamer elements for gst_viewer. Currently decodes the stream and renders the video on the display.
* Line 248: `res = thetauvc_get_stream_ctrl_format_size(...)` 	- Defines the streaming settings of the camera. THETAUVC_MODE_FHD_2997 = 2K, THETAUVC_MODE_UHD_2997 = 4K. Currently 2K is recommended to ensure realtime performance

## Other useful documentation
Webpage for resources on Ricoh Development on Linux: [https://codetricity.github.io/theta-linux/](https://codetricity.github.io/theta-linux/)
Theta community forum page for live streaming Ricoh Theta over USB on Linux: [https://community.theta360.guide/t/live-streaming-over-usb-on-ubuntu-and-linux-nvidia-jetson/4359](https://community.theta360.guide/t/live-streaming-over-usb-on-ubuntu-and-linux-nvidia-jetson/4359)



