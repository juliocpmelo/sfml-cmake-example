cmake_minimum_required(VERSION 3.19)
project("Sfm Example")

set (BUILD_SHARED_LIBS FALSE)
add_subdirectory(./SFML-2.5.1)

include_directories(./SFML-2.5.1/include)

add_executable(compile_code
               main.cpp)

target_link_libraries(compile_code sfml-main sfml-graphics sfml-audio)

#copy openal32.dll to local build path, if you built a 64 binary, you might needed to change here
add_custom_target(
    sfml_test
    COMMAND  ${CMAKE_COMMAND} -E copy ${CMAKE_SOURCE_DIR}/SFML-2.5.1/extlibs/bin/x86/openal32.dll ${CMAKE_CURRENT_BINARY_DIR}
    COMMENT "Copy dll file to ${CMAKE_CURRENT_BINARY_DIR} directory" VERBATIM
    DEPENDS compile_code
)
