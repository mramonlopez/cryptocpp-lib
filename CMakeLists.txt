cmake_minimum_required(VERSION 3.6)

set(lib_name cryptopp)
set(target_name ${lib_name})

project(${lib_name})

if(IOS)
    set(platform_name ios)
    set(platform_spec_path ios/lib)
elseif(ANDROID)
    set(platform_name android)
    set(platform_spec_path android/lib/${ANDROID_ABI})
endif()

add_library(${target_name} STATIC IMPORTED GLOBAL)

set_target_properties(${target_name} PROPERTIES
    INTERFACE_INCLUDE_DIRECTORIES "${CMAKE_CURRENT_SOURCE_DIR}/${platform_name}/include"
)

set_target_properties(${target_name} PROPERTIES
    IMPORTED_LOCATION "${CMAKE_CURRENT_SOURCE_DIR}/${platform_spec_path}/lib${lib_name}.a"
)
