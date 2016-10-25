cmake_minimum_required(VERSION 2.8 FATAL_ERROR)
project(cmake-base-qt)

set(CMAKE_RUNTIME_OUTPUT_DIRECTORY "${CMAKE_BINARY_DIR}/bin")
set(CMAKE_ARCHIVE_OUTPUT_DIRECTORY "${CMAKE_BINARY_DIR}/lib")
set(CMAKE_LIBRARY_OUTPUT_DIRECTORY "${CMAKE_BINARY_DIR}/lib")

set(CPACK_PACKAGE_CONTACT "Foo Bar")
set(CPACK_PACKAGE_DESCRIPTION_SUMMARY "CMake base structure for standard C++ projects relying on Qt")
set(CPACK_PACKAGE_VERSION_MAJOR 1)
set(CPACK_PACKAGE_VERSION_MINOR 0)
set(CPACK_PACKAGE_VERSION_PATCH 0)
set(CPACK_PACKAGE_VERSION "${CPACK_PACKAGE_VERSION_MAJOR}.${CPACK_PACKAGE_VERSION_MINOR}.${CPACK_PACKAGE_VERSION_PATCH}")

include(CPack)
include(CTest)

# Find Qt5 components
set(Qt5_Components
	Core
	Widgets)

# Load each Qt5 component
foreach(Qt5_Component ${Qt5_Components})
	find_package(Qt5${Qt5_Component})
endforeach()

# Tell CMake to run moc when necessary:
set(CMAKE_AUTOMOC ON)

# As moc files are generated in the binary dir, tell CMake
# to always look for includes there:
set(CMAKE_INCLUDE_CURRENT_DIR ON)

add_subdirectory(src)
add_subdirectory(test)
