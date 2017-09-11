cmake_minimum_required(VERSION 3.5)
project(ros_workspace)

find_package(ament_cmake_core REQUIRED)

set(ament_cmake_package_templates_ENVIRONMENT_HOOK_PYTHONPATH "${CMAKE_INSTALL_PREFIX}/lib/python3.5/site-packages/ament_package/template/environment_hook/pythonpath.sh.in")
ament_environment_hooks("${ament_cmake_package_templates_ENVIRONMENT_HOOK_PYTHONPATH}")
ament_package()
ament_generate_environment()

