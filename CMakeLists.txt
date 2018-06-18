cmake_minimum_required(VERSION 3.5)
project(ros_workspace)

find_package(ament_cmake_core REQUIRED)

# Collect current python 3 version
execute_process(COMMAND python3 -c "from distutils import sysconfig; print(sysconfig.get_python_version())" OUTPUT_VARIABLE PYTHON_MAJOR_MINOR OUTPUT_STRIP_TRAILING_WHITESPACE)
set(PYTHON_INSTALL_DIR "lib/python${PYTHON_MAJOR_MINOR}/site-packages")
set(ament_cmake_package_templates_ENVIRONMENT_HOOK_PYTHONPATH "${CMAKE_INSTALL_PREFIX}/${PYTHON_INSTALL_DIR}/ament_package/template/environment_hook/pythonpath.sh.in")
ament_environment_hooks("${ament_cmake_package_templates_ENVIRONMENT_HOOK_PYTHONPATH}")

# Collect machine architecture triplet for libraries using GNU install dirs.
execute_process(COMMAND gcc -dumpmachine OUTPUT_VARIABLE MULTIARCH_TRIPLET OUTPUT_STRIP_TRAILING_WHITESPACE)
ament_environment_hooks(library_paths.sh.in)

ament_package()
ament_generate_environment()

