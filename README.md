# libuvc-theta-sample
## gst/gst_viewer
Decode and display sample using gstreamer. You may need gstreamer1.0 develpment packages to build and run.

## gst/gst_loopback
Feed decoded video to the v4l2loopback device so that v4l2-based application can use THETA video without modification.

CAUTION: gst_loopback may not run on all platforms, as decoder to v4l2loopback pipeline configuration is platform dependent

## Lines of note:
* Line 188: `pipe_proc = ....` - Defines the gstreamer elements for gst_loopback. Currently decodes the stream and directs it to v4l2sink to render video on /dev/video1
* Line 192: `pipe_proc = ....` - Defines the gstreamer elements for gst_viewer. Currently decodes the stream and renders the video on the display.
* Line 248: `res = thetauvc_get_stream_ctrl_format_size(...)` 	- Defines the streaming settings of the camera. THETAUVC_MODE_FHD_2997 = 2K, THETAUVC_MODE_UHD_2997 = 4K. Currently 2K is recommended to ensure realtime performance

