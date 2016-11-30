cmake_minimum_required(VERSION 2.6.3)
project(gst-rtsp-library)

set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++11 -Wall")

list(APPEND CMAKE_MODULE_PATH "${CMAKE_CURRENT_LIST_DIR}/cmake")

find_package(GLib REQUIRED)
find_package(GStreamer REQUIRED)

include_directories("gst-rtsp-server")
include_directories("${GLIB_INCLUDE_DIRS}")
include_directories("${GSTREAMER_INCLUDE_DIRS}")
include_directories("${GSTREAMER_BASE_INCLUDE_DIRS}")
include_directories("${GSTREAMER_RTSP_INCLUDE_DIRS}")

add_library(gstrtsplibrary

  gst-rtsp-server/gst/rtsp-server/rtsp-address-pool.c
  gst-rtsp-server/gst/rtsp-server/rtsp-media-factory-uri.c
  gst-rtsp-server/gst/rtsp-server/rtsp-params.c
  gst-rtsp-server/gst/rtsp-server/rtsp-session-media.c
  gst-rtsp-server/gst/rtsp-server/rtsp-auth.c
  gst-rtsp-server/gst/rtsp-server/rtsp-stream.c
  gst-rtsp-server/gst/rtsp-server/rtsp-media-factory.c
  gst-rtsp-server/gst/rtsp-server/rtsp-permissions.c
  gst-rtsp-server/gst/rtsp-server/rtsp-session-pool.c
  gst-rtsp-server/gst/rtsp-server/rtsp-thread-pool.c
  gst-rtsp-server/gst/rtsp-server/rtsp-client.c
  gst-rtsp-server/gst/rtsp-server/rtsp-media.c
  gst-rtsp-server/gst/rtsp-server/rtsp-sdp.c
  gst-rtsp-server/gst/rtsp-server/rtsp-session.c
  gst-rtsp-server/gst/rtsp-server/rtsp-token.c
  gst-rtsp-server/gst/rtsp-server/rtsp-context.c
  gst-rtsp-server/gst/rtsp-server/rtsp-mount-points.c
  gst-rtsp-server/gst/rtsp-server/rtsp-server.c
  gst-rtsp-server/gst/rtsp-server/rtsp-stream-transport.c
)

set(GSTREAMER_LIBS

  gstreamer-1.0
  gstbase-1.0
  gstrtp-1.0
  gstsdp-1.0
  gstrtsp-1.0
  gstapp-1.0
  gstnet-1.0
  gobject-2.0
  gmodule-2.0
  xml2
  gthread-2.0
  glib-2.0
  gio-2.0
)
target_link_libraries(gstrtsplibrary "${GSTREAMER_LIBS}")

get_directory_property(hasParent PARENT_DIRECTORY)
if(hasParent)
  set(GST_RTSP_SERVER_INCLUDE_DIRS

    "${GLIB_INCLUDE_DIRS}"
    "${GSTREAMER_INCLUDE_DIRS}"
    "${GSTREAMER_BASE_INCLUDE_DIRS}"
    "${GSTREAMER_RTSP_INCLUDE_DIRS}"

    PARENT_SCOPE
  )
endif()
