##---------------------------------------------------------------------------
## Author:      Jorgen Bodde
## Copyright:   (c) Jorgen Bodde
## License:     wxWidgets License
## Update:      2008/12 by Werner Smekal
##---------------------------------------------------------------------------

# define minimum cmake version
cmake_minimum_required(VERSION 2.6.2)

# Our project is called 'ode' this is how it will be called in
# visual studio, and in our makefiles. 
project(ode)

# Location where cmake first looks for cmake modules.
set(CMAKE_MODULE_PATH "${PROJECT_SOURCE_DIR}")

##---------------------------------------------------
## Please set your wxWidgets configuration here
##--------------------------------------------------- 
 
# Here you can define what libraries of wxWidgets you need for your
# application. You can figure out what libraries you need here;
# https://www.wxwidgets.org/manuals/2.8/wx_librarieslist.html
# We need the Find package for wxWidgets to work
# NOTE: if you're using aui, include aui in this required components list.

# It was noticed that when using MinGW gcc it is essential that 'core' is mentioned before 'base'.
find_package(wxWidgets COMPONENTS core base REQUIRED)
 
##---------------------------------------------------
## Actual config file starts here
##--------------------------------------------------- 
 
# wxWidgets include (this will do all the magic to configure everything)
include( "${wxWidgets_USE_FILE}" )

# For convenience we define the sources as a variable. You can add 
# header files and cpp/c files and CMake will sort them out
set(SRCS ode.cpp)

# If we build for windows systems, we also include the resource file
# containing the manifest, icon and other resources
if(WIN32)
  set(SRCS ${SRCS} ode.rc)
endif(WIN32)

# Here we define the executable ode.exe or ode on other systems
# the above paths and defines will be used in this build
add_executable(ode WIN32 ${SRCS})

# We add to our target 'ode' the wxWidgets libraries. These are
# set for us by the find script. If you need other libraries, you
# can add them here as well. 
target_link_libraries(ode ${wxWidgets_LIBRARIES})
