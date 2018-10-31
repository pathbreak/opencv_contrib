set(the_description "Object Detection")

# 3.4.3-corrections: Removing "OPTIONAL opencv_highgui" since it's only used by samples
# and highgui is automatically included when building samples.
ocv_define_module(dpm opencv_core opencv_imgproc opencv_objdetect WRAP python)

ocv_warnings_disable(CMAKE_CXX_FLAGS /wd4512) # disable warning on Win64
