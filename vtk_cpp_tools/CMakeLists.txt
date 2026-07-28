# http://www.vtk.org/Wiki/VTK/Tutorials/CMakeListsFile
cmake_minimum_required(VERSION 3.5...4.4)
project(mindboggle_surfaces)
find_package(VTK REQUIRED COMPONENTS
  CommonCore
  CommonDataModel
)

## Rather than set the VTK_DIR, compile with
## "cmake .. -DVTK_DIR:STRING=/Users/arno/anaconda/lib/cmake/vtk-7.0"
#set(VTK_DIR "/Users/arno/anaconda/lib/cmake/vtk-7.0")

#if(COMMAND CMAKE_POLICY)
#  CMAKE_POLICY(SET CMP0003 NEW)
#endif(COMMAND CMAKE_POLICY)

# David Gobbi on vtkusers mailing list:
# For building a binary package to share with others,
# set to a reasonably old deployment target (e.g. 10.7) and SDK (e.g. 10.9):
#set(CMAKE_OSX_DEPLOYMENT_TARGET "10.7")
#set(CMAKE_OSX_SYSROOT "macosx10.9")

add_subdirectory(
travel_depth
)

add_subdirectory(
curvature
)

add_subdirectory(
surface_overlap
)

add_subdirectory(
area
)

add_subdirectory(
gradient
)

add_subdirectory(
geodesic_depth
)

#add_subdirectory(
#medial_surfaces
#)

add_library(MeshAnalyser MeshAnalyser.cpp)
target_link_libraries(MeshAnalyser PUBLIC VTK::CommonCore VTK::CommonDataModel)

add_library(FsSurfaceReader FsSurfaceReader.cpp)
target_link_libraries(FsSurfaceReader PUBLIC VTK::CommonCore VTK::CommonDataModel)

add_library(VtkFileEditor VtkFileEditor.cpp)
target_link_libraries(VtkFileEditor PUBLIC VTK::CommonCore VTK::CommonDataModel)

add_library(TravelDepth TravelDepth.cpp)
target_link_libraries(TravelDepth PUBLIC VTK::CommonCore VTK::CommonDataModel)

add_library(GradientComputer GradientComputer.cpp)
target_link_libraries(GradientComputer PUBLIC VTK::CommonCore VTK::CommonDataModel)

add_library(PointAreaComputer PointAreaComputer.cpp)
target_link_libraries(PointAreaComputer PUBLIC VTK::CommonCore VTK::CommonDataModel)

add_library(Overlap Overlap.cpp)
target_link_libraries(Overlap PUBLIC PointAreaComputer VTK::CommonCore VTK::CommonDataModel)