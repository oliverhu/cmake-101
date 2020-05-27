cmake_minimum_required(VERSION 2.8.9)
project(directory_static_test)
set(CMAKE_BUILD_TYPE Release)

#Bring the headers, such as Student.h into the project
# include_directories(include)

#However, the file(GLOB...) allows for wildcard additions:
file(GLOB SOURCES "src/*.cpp")

#Generate the static library from the sources
add_library(testStudentStatic STATIC ${SOURCES})

target_include_directories(testStudentStatic PUBLIC include)

#Set the location for library installation -- i.e., /usr/lib in this case
# not really necessary in this example. Use "sudo make install" to apply
install(TARGETS testStudentStatic DESTINATION /usr/lib)