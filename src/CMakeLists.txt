add_subdirectory(common)

target_sources(debayer PRIVATE 
    cuda_debayer.cpp
    bayer2rgb.cu
    camera_device.cpp
    gl_display.cpp
)

target_include_directories(debayer PRIVATE
    ${CMAKE_SOURCE_DIR}/include
)

target_include_directories(debayer PUBLIC /usr/include ${OPENGL_INCLUDE_DIRS}  ${GLUT_INCLUDE_DIRS} )


# the following line shouldn't be necessary as target_link_libraries
# with OpenMP::OpenMP_CXX should pass the correct flags for OpenMP
# but apparently, this is KO when using nvcc :(
# You can remove that if OpenMP is not required
# checked using cmake 3.14.3 (October 2019)
target_compile_options(debayer PUBLIC
  $<$<COMPILE_LANGUAGE:CXX>:${OpenMP_CXX_FLAGS}>
  $<$<COMPILE_LANGUAGE:CUDA>:-Xcompiler ${OpenMP_CXX_FLAGS}>
  )

#target_link_libraries(debayer PUBLIC CUDA::cublas)
#target_link_libraries(debayer PUBLIC OpenMP::OpenMP_CXX)
#target_link_libraries(debayer PUBLIC cuda::common)


target_link_libraries(debayer ${OPENGL_LIBRARIES} ${GLUT_LIBRARY} ${GLEW_LIBRARIES} -lGL -lglut -lGLEW)
