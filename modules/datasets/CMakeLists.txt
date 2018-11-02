set(the_description "datasets framework")

set(filter_srcs "${CMAKE_CURRENT_LIST_DIR}/src/tinyxml2/tinyxml2.cpp")
if(CMAKE_CXX_COMPILER_ID STREQUAL "GNU")
  ocv_append_source_files_cxx_compiler_options(filter_srcs "-Wno-suggest-override")  # GCC
elseif(CMAKE_CXX_COMPILER_ID STREQUAL "Clang")
  ocv_append_source_files_cxx_compiler_options(filter_srcs "-Wno-inconsistent-missing-override")  # Clang
endif()

ocv_define_module(datasets opencv_core opencv_imgcodecs WRAP python)

if(BUILD_EXAMPLES)
  ocv_add_dependencies(opencv_datasets opencv_ml opencv_flann opencv_text)
endif()

ocv_warnings_disable(CMAKE_CXX_FLAGS
    /wd4267                                      # flann, Win64
    -Wimplicit-fallthrough                       # tinyxml2.cpp
)
