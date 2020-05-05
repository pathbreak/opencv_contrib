set(the_description "Contributed/Experimental Algorithms for Salient 2D Features Detection")

if(HAVE_CUDA)
  ocv_warnings_disable(CMAKE_CXX_FLAGS -Wundef)
endif()
ocv_add_module(xfeatures2d opencv_core opencv_imgproc opencv_features2d OPTIONAL opencv_calib3d opencv_shape opencv_ml opencv_cudaarithm WRAP python java)

set(xfeatures2d_hdrs
    ${CMAKE_CURRENT_LIST_DIR}/src/precomp.hpp
    )

set(xfeatures2d_srcs
    ${CMAKE_CURRENT_LIST_DIR}/src/gms.cpp
    ${CMAKE_CURRENT_LIST_DIR}/src/logos.cpp
    )

file(GLOB xfeatures2d_logos_srcs
     "${CMAKE_CURRENT_LIST_DIR}/src/logos/*.cpp"
     )
    
file(GLOB xfeatures2d_ext_hdrs
     "${CMAKE_CURRENT_LIST_DIR}/include/opencv2/*.hpp"
     "${CMAKE_CURRENT_LIST_DIR}/include/opencv2/${name}/*.hpp"
     "${CMAKE_CURRENT_LIST_DIR}/include/opencv2/${name}/*.h")

source_group("Src" FILES ${xfeatures2d_srcs} ${xfeatures2d_hdrs} ${xfeatures2d_logos_srcs})
source_group("Include" FILES ${xfeatures2d_ext_hdrs})
ocv_set_module_sources(HEADERS ${xfeatures2d_ext_hdrs} SOURCES ${xfeatures2d_srcs} ${xfeatures2d_logos_srcs} ${xfeatures2d_hdrs})
ocv_module_include_directories()

ocv_create_module()

#include(${CMAKE_CURRENT_SOURCE_DIR}/cmake/download_vgg.cmake)
#include(${CMAKE_CURRENT_SOURCE_DIR}/cmake/download_boostdesc.cmake)
#set(DOWNLOAD_DIR "${OpenCV_BINARY_DIR}/downloads/xfeatures2d")
#download_boost_descriptors("${DOWNLOAD_DIR}" boost_status)
#download_vgg_descriptors("${DOWNLOAD_DIR}" vgg_status)
#if(NOT boost_status OR NOT vgg_status)
#  ocv_module_disable(xfeatures2d)
#endif()

#ocv_module_include_directories("${DOWNLOAD_DIR}")

if(TARGET opencv_test_${name})
  ocv_target_include_directories(opencv_test_${name} "${OpenCV_SOURCE_DIR}/modules")  # use common files from features2d tests
endif()
