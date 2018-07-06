cmake_minimum_required(VERSION 3.5)
project(fail)

set(fail_MAJOR_VERSION 0)
set(fail_MINOR_VERSION 0)
set(fail_PATCH_VERSION 0)
set(fail_VERSION
  ${fail_MAJOR_VERSION}.${fail_MINOR_VERSION}.${fail_PATCH_VERSION})

# Default to C99
if(NOT CMAKE_C_STANDARD)
  set(CMAKE_C_STANDARD 99)
endif()

# Default to C++14
if(NOT CMAKE_CXX_STANDARD)
  set(CMAKE_CXX_STANDARD 14)
endif()

if(CMAKE_COMPILER_IS_GNUCXX OR CMAKE_CXX_COMPILER_ID MATCHES "Clang")
  add_compile_options(-Wall -Wextra -Wpedantic)
endif()


find_package(rosidl_default_generators REQUIRED)
find_package(std_msgs REQUIRED)

rosidl_generate_interfaces(${PROJECT_NAME}
        msg/Test.msg
        srv/Test.srv
        DEPENDENCIES std_msgs
        )

add_executable(fail src/main.c)
install(TARGETS fail DESTINATION share/bin)

# uncomment the following section in order to fill in
# further dependencies manually.
# find_package(<dependency> REQUIRED)
