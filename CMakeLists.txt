cmake_minimum_required(VERSION 3.25 FATAL_ERROR)

#Defino el nombre del proyecto, la versión y la descripción
project(
    "FirstProjectInCMake"
    VERSION 1.0.0
    DESCRIPTION "CMake C Project Template for Operating Systems II"
    LANGUAGES C
)

#Defino el estándar de C que se utilizará
set(CMAKE_C_STANDARD 17)

#Defino el directorio de donde se incluirán los archivos de cabecera
include_directories(include)

#Defino el directorio de donde se tomarán los archivos de código fuente
file(GLOB_RECURSE SOURCES "src/*.c")

#Defino el ejecutable que se generará, con los datos que cargué anteriormente
add_executable(${PROJECT_NAME} ${SOURCES})
