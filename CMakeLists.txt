cmake_minimum_required(VERSION 2.8 FATAL_ERROR)

project(point-cloud)

find_package(PCL 1.3 REQUIRED )
find_package (Qt4 REQUIRED)
find_package (VTK REQUIRED)
find_package (PCL 1.7.1 REQUIRED)

include_directories (${PCL_INCLUDE_DIRS})
link_directories    (${PCL_LIBRARY_DIRS})
add_definitions     (${PCL_DEFINITIONS})

set  (project_SOURCES main.cpp pclviewer.cpp)
set  (project_HEADERS pclviewer.h)
set  (project_FORMS   pclviewer.ui)
set  (VTK_LIBRARIES   vtkRendering vtkGraphics vtkHybrid QVTK)
set  (CMAKE_AUTOUIC on) 

QT4_WRAP_CPP (project_HEADERS_MOC   ${project_HEADERS})
QT4_WRAP_UI  (project_FORMS_HEADERS ${project_FORMS})
INCLUDE         (${QT_USE_FILE})
ADD_DEFINITIONS (${QT_DEFINITIONS})

add_executable (gen_pcd gen_pcd.cpp)
add_executable (pcviewer ${project_SOURCES} ${project_FORMS_HEADERS} ${project_HEADERS_MOC})

target_link_libraries(gen_pcd ${PCL_COMMON_LIBRARIES} ${PCL_IO_LIBRARIES})
target_link_libraries (pcviewer ${QT_LIBRARIES} ${PCL_LIBRARIES} ${VTK_LIBRARIES})








