cmake_minimum_required(VERSION 3.5)
project(ros_workspace NONE)

find_package(ament_cmake_core REQUIRED)

# Collect current python 3 version
execute_process(COMMAND python3 -c "from distutils import sysconfig; print(sysconfig.get_python_version())" OUTPUT_VARIABLE PYTHON_MAJOR_MINOR OUTPUT_STRIP_TRAILING_WHITESPACE)

# Locate ament_package template files.
set(PYTHON_INSTALL_DIR "lib/python${PYTHON_MAJOR_MINOR}/site-packages")
set(AMENT_PACKAGE_TEMPLATE_DIR "${CMAKE_INSTALL_PREFIX}/${PYTHON_INSTALL_DIR}/ament_package/template")
set(ament_package_templates_environment_hook_librarypath "${AMENT_PACKAGE_TEMPLATE_DIR}/environment_hook/librarypath.sh.in")
set(ament_package_templates_environment_hook_pythonpath "${AMENT_PACKAGE_TEMPLATE_DIR}/environment_hook/pythonpath.sh.in")

# Set environment hooks for default environment.
ament_environment_hooks("${ament_cmake_package_templates_environment_hook_librarypath}")
ament_environment_hooks("${ament_cmake_package_templates_environment_hook_pythonpath}")


ament_package()
ament_generate_environment()

