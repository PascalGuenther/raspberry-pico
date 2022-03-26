cmake_minimum_required(VERSION 3.13)


if(NOT DEFINED PICO_SDK_PATH)
set(PICO_SDK_PATH ${CMAKE_CURRENT_SOURCE_DIR}/pico-sdk)
endif()

if(NOT DEFINED PICO_EXTRAS_PATH)
set(PICO_EXTRAS_PATH ${CMAKE_CURRENT_SOURCE_DIR}/pico-extras)
endif()

# Pull in PICO SDK (must be before project)
include(${PICO_SDK_PATH}/external/pico_sdk_import.cmake)

project(RP2040)
pico_sdk_init()

option(BUILD_DOOM "Build doom game" OFF)
if(BUILD_DOOM)
    add_subdirectory(rp2040-doom)
endif()

option(BUILD_PICOTOOL "Build picotool for interacting with a RP2040 device in BOOTSEL mode (requires libusb)" OFF)
if(BUILD_PICOTOOL)
    if((NOT DEFINED PC_LIBUSB_INCLUDEDIR) AND ((NOT DEFINED PC_LIBUSB_INCLUDEDIR)))
    set(PC_LIBUSB_INCLUDEDIR ${CMAKE_CURRENT_SOURCE_DIR}/libusb/include/libusb-1.0)
    set(PC_LIBUSB_LIBDIR ${CMAKE_CURRENT_SOURCE_DIR}/libusb/VS2019/MS32/static)
    endif()

    add_subdirectory(picotool)
endif()
