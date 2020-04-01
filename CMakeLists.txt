# This is an example of using common_utils and common_cmake_modules
#
# Required, and this line has to go atop. 3.15 is recommended, and 3.12 will
# probably work.
cmake_minimum_required(VERSION 3.15)

# Required. This set the project name
project(common_utils_boilerplate LANGUAGES CXX C)

# Required. This set the necessary global settings and load
# the helps for adding dependencies defined in common_cmake_modules
include("${CMAKE_CURRENT_SOURCE_DIR}/common_utils/cmake/CommonSettings.cmake")

# Actually add dependencies
# See common_cmake_modules/*.cmake for available items.
# The name here should match the filename stem of the CMake file there.
include(SpdlogAndFmt)
if (VERBOSE)  # VERBOSE is defined in CommonSettings.cmake
    # This is defined in CommonSettings and can be used to
    # display info of a target.
    print_target_properties(spdlog::spdlog)
    print_target_properties(fmt::fmt)
endif()

# The below is just normal cmake code.
# Notice the usage of imported targets, which are made available through
# the common_cmake_modules and the include(...) above.
# Also, note that we didn't handle the common_utils header only code here,
# which is done by directly symlink the common_utils/src/utils folder to
# appropriate location so in the cpp file one can do
# #include <utils/xxx.h>

add_executable(hello_world)
target_sources(hello_world
    PRIVATE
        hello_world.cpp
        )
target_link_libraries(hello_world
    PRIVATE
        spdlog::spdlog
        fmt::fmt
    )
