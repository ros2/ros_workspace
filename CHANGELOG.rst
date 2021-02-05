^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
Changelog for package ros_workspace
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

1.0.2 (2021-02-04)
------------------
* Use GNUInstallDirs to determine multiarch library dir (`#20 <https://github.com/ros2/ros_workspace/issues/20>`_)
* Contributors: Scott K Logan

1.0.1 (2020-06-05)
------------------
* set flag to skip parent_prefix_path (`#19 <https://github.com/ros2/ros_workspace/issues/19>`_)
* Contributors: Dirk Thomas

1.0.0 (2020-05-12)
------------------
* Extend library path to have multiarch directory (`#18 <https://github.com/ros2/ros_workspace/issues/18>`_)
* Enable Windows build. (`#17 <https://github.com/ros2/ros_workspace/issues/17>`_)
* Contributors: Jacob Perron, Sean Yen

0.8.0 (2019-10-11)
------------------
* Added .dsv file generation for PYTHONPATH. (`#16 <https://github.com/ros2/ros_workspace/issues/16>`_)
* Added support for ament_package installed with setup.py develop. (`#15 <https://github.com/ros2/ros_workspace/issues/15>`_)
* Contributors: Dirk Thomas

0.7.1 (2019-04-29)
------------------
* Reverted adding the COLCON_PREFIX_PATH env var. (`#14 <https://github.com/ros2/ros_workspace/issues/14>`_)
* Contributors: Dirk Thomas

0.7.0 (2019-04-08)
------------------
* Add LICENSE file containing full Apache 2.0 license text. (`#13 <https://github.com/ros2/ros_workspace/issues/13>`_)
* Contributors: Steven! Ragnarök

0.6.1 (2019-02-07)
------------------
* Add COLCON_PREFIX_PATH env hook. (`#11 <https://github.com/ros2/ros_workspace/issues/11>`_)
* Contributors: Dirk Thomas

0.6.0 (2018-11-14)
------------------
* Set default environment hooks for PATH, PYTHONPATH, and LD_LIBRARY_PATH. (`#10 <https://github.com/ros2/ros_workspace/issues/10>`_)
  * Drop setting multiarch library by default.
  Installing into a multiarch dir when specifying a non-standard Debian
  package root appears to have been a bug that was fixed in the Bionic
  toolchain.
  Packages that used to require special handling because their libraries
  were placed in, for example, /opt/ros/bouncy/lib/x86_64-linux-gnu/ now
  place their libraries directly in /opt/ros/bouncy/lib.
  Since this is no longer the default, we should not set any default
  environment hooks using that directory.
  Packages which want to explicitly make use of a multiarch library path
  should set their own environment hooks.
  * Add default environment hook for the binary path.
* set language to NONE as this doesnt compile any code (`#9 <https://github.com/ros2/ros_workspace/issues/9>`_)
* Contributors: Mikael Arguedas, Steven! Ragnarök

0.5.1 (2018-06-18)
------------------
* Merge pull request `#6 <https://github.com/ros2/ros_workspace/issues/6>`_ from ros2/add-default-load-path-unconditionially
  Add default load path unconditionially
* Add note about default environment hooks and link to further issue.
* Add /opt/ros/rosdistro/lib to default library path.
  Previously this library path was added to LD_LIBRARY_PATH by environment
  hooks in other packages. However this means that pure-CMake packages
  which don't depend on ament libraries and do not set environment hooks
  of their own aren't found by dependents which are also pure cmake.
  An example of this is fastrtps and fastcdr, both of which are
  third-party cmake packages which do not register environment hooks.
  This bug was previously masked for fastrtps and fastcdr but a
  mis-applied dependency on ament_cmake rather than cmake in fastrtps.
* Rename hook shell script.
  Since we'll be modifying this to include an additional library path the
  name needs an update.
* Contributors: Steven! Ragnarök

0.5.0 (2018-06-13)
------------------
* Merge pull request `#5 <https://github.com/ros2/ros_workspace/issues/5>`_ from ros2/ament-package-dependency
  Add direct build dependency on ament_package.
* Add direct build dependency on ament_package.
  This dependency was previously implied by the dependency on
  ament_cmake_core. Since we directly use environment script templates
  from ament_package let's make that direct dependency explicit.
* Merge pull request `#4 <https://github.com/ros2/ros_workspace/issues/4>`_ from nuclearsandwich/fetch-python-version
  Collect python version to use in pythonpath hook.
* Collect python version to use in pythonpath hook.
  Initially this was hardcoded. Since the python minor version depends on
  the target platform this will fetch it from the available python3
  binary.
* Merge pull request `#2 <https://github.com/ros2/ros_workspace/issues/2>`_ from nuclearsandwich/cleaner-environment-hooks
  Install gnuinstalldirs library hook as a generic environment hook.
* Install gnuinstalldirs library hook as a generic environment hook.
* Contributors: Steven! Ragnarök

0.4.0 (2017-12-08)
------------------
* Fix trailing whitespace bug and drop unneeded export.
* Add an environment hook to use the platform triplet in library_path.
* Add really hacky support for gnuinstalldirs.
* Bump to 0.0.3 for beta 3.
* Fix the python path bug but only for real.
* Explicitly set python installation path for the template.
* Bump to 0.0.2 for consistency.
* Set the root pythonpath.
  Python packages (at the moment, specifically ament_package) are not
  setting their ament_index resources, so nothing is in the PYTHONPATH for
  those packages. This does some really quite awful things in order to set
  a release-wide "default" python path. I have no doubt that this is
  brittle and that better alternatives (including fixing python package
  ament resources) should be implemented.
* workspace => ros_workspace
* Be an ament package in order to make sure package index exists.
* This might not be enough, but it might be just enough.
* Contributors: Steven! Ragnarök, Steven! Ragnarök
