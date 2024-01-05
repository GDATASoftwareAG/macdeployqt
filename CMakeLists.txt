cmake_minimum_required(VERSION 3.23)

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

project(macdeployqt)

find_package(Qt6 REQUIRED COMPONENTS Core)

set(MACDEPLOYQT_RPATH "@executable_path/../lib" CACHE STRING "RPATH in the resulting macdeployqt binary.")

add_executable(macdeployqt
    src/main.cpp
    src/shared.cpp
    src/shared.h
    )

target_link_libraries(macdeployqt
    PRIVATE
    Qt6::Core
    "-framework CoreFoundation"
    )

set_target_properties(macdeployqt PROPERTIES
    INSTALL_RPATH "${MACDEPLOYQT_RPATH}"
    )

install(TARGETS macdeployqt
    RUNTIME DESTINATION .
    )
