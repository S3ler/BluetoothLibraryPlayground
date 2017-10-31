cmake_minimum_required(VERSION 3.7)
project(SimpleBluetoothLowEnergySocketNUSCentral)

set(CMAKE_CXX_STANDARD 14)


find_package(PkgConfig REQUIRED)

# thank you: https://stackoverflow.com/questions/38515316/how-to-configure-dbus-dependencies-with-cmake
set(CMAKE_MODULE_PATH ${CMAKE_CURRENT_SOURCE_DIR})
find_package(DBus REQUIRED)
include_directories(${DBUS_INCLUDE_DIRS})

pkg_search_module(GLIB REQUIRED glib-2.0)
include_directories(${GLIB_INCLUDE_DIRS})

add_subdirectory(lib/SimpleBluetoothLowEnergySocket)

include_directories(lib/SimpleBluetoothLowEnergySocket/libBLE)
include_directories(lib/SimpleBluetoothLowEnergySocket/libBLE/gdbus)
include_directories(lib/SimpleBluetoothLowEnergySocket/libBLE/helper)
include_directories(lib/SimpleBluetoothLowEnergySocket/libBLE/proxy)


set(MAIN_FILE main.cpp)
add_executable(SimpleBluetoothLowEnergySocketNUSCentral ${MAIN_FILE})
target_link_libraries(SimpleBluetoothLowEnergySocketNUSCentral libBLE)