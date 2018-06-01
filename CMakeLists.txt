cmake_minimum_required(VERSION 3.5)
project(ros_workspace)

find_package(ament_cmake_core REQUIRED)

set(PYTHON_INSTALL_DIR "lib/python3.6/site-packages")
set(ament_cmake_package_templates_ENVIRONMENT_HOOK_PYTHONPATH "${CMAKE_INSTALL_PREFIX}/${PYTHON_INSTALL_DIR}/ament_package/template/environment_hook/pythonpath.sh.in")
ament_environment_hooks("${ament_cmake_package_templates_ENVIRONMENT_HOOK_PYTHONPATH}")

# We create the library_path.sh file via ament only to overwrite it so that it is properly registered as an ament hook.
set(ament_cmake_package_templates_ENVIRONMENT_HOOK_LIBRARY_PATH "${CMAKE_INSTALL_PREFIX}/${PYTHON_INSTALL_DIR}/ament_package/template/environment_hook/library_path.sh")
ament_environment_hooks("${ament_cmake_package_templates_ENVIRONMENT_HOOK_LIBRARY_PATH}")

ament_package()
ament_generate_environment()

execute_process(COMMAND gcc -dumpmachine OUTPUT_VARIABLE MULTIARCH_TRIPLET OUTPUT_STRIP_TRAILING_WHITESPACE)
configure_file(gnuinstalldirs_environment_hook_library_path.sh.in "${PROJECT_BINARY_DIR}/gnuinstalldirs_environment_hook_library_path.sh" @ONLY)
install(FILES ${PROJECT_BINARY_DIR}/gnuinstalldirs_environment_hook_library_path.sh DESTINATION  "${CMAKE_INSTALL_PREFIX}/share/ros_workspace/environment" RENAME library_path.sh)

