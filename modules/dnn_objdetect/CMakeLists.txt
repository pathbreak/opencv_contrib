set(the_description "Post-Processing for Object Detection using CNNs")

ocv_define_module(dnn_objdetect opencv_core)

if(BUILD_EXAMPLES)
  ocv_add_dependencies(opencv_dnn_objdetect  opencv_imgproc  opencv_dnn)
endif()

