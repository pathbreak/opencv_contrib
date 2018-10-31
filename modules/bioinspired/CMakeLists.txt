set(the_description "Biologically inspired algorithms")
ocv_warnings_disable(CMAKE_CXX_FLAGS -Wundef)

# 3.4.3-corrections: Removing "OPTIONAL opencv_highgui" since it's only used by samples
# and highgui is automatically included when building samples.
ocv_define_module(bioinspired opencv_core OPTIONAL opencv_ocl WRAP java python)

if(BUILD_EXAMPLES)
  ocv_add_dependencies(opencv_bioinspired  opencv_imgproc)
endif()
