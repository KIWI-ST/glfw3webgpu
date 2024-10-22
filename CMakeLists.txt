add_library(glfw3webgpu STATIC glfw3webgpu.c)
target_include_directories(glfw3webgpu PUBLIC .)
target_include_directories(glfw3webgpu PUBLIC ${Dawn_BINARY_DIR}/gen/include/)
target_include_directories(glfw3webgpu PUBLIC ${Dawn_BINARY_DIR}/gen/include/dawn/webgpu.h)
target_link_libraries(glfw3webgpu PUBLIC glfw webgpu_dawn)

if(WIN32)
    target_compile_definitions(glfw3webgpu PRIVATE _GLFW_WIN32)
elseif(APPLE AND NOT IOS)
    # osx
    target_compile_definitions(glfw3webgpu PRIVATE _GLFW_COCOA)
    target_compile_options(glfw3webgpu PRIVATE -x objective-c)
    target_link_libraries(glfw3webgpu PRIVATE "-framework Cocoa" "-framework CoreVideo" "-framework IOKit" "-framework QuartzCore")
elseif(APPLE AND IOS)
    # ios
    target_compile_definitions(glfw3webgpu PRIVATE _GLFW_COCOA)
elseif(X11)
    # linux x11
    target_compile_definitions(glfw3webgpu PRIVATE _GLFW_X11)
elseif(WAYLAND)
    # linux wayland
    target_compile_definitions(glfw3webgpu PRIVATE _GLFW_WAYLAND)
endif()
