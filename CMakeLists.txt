cmake_minimum_required(VERSION 3.25 FATAL_ERROR)

#Defino el nombre del proyecto, la versión y la descripción
project(
    "FirstProjectInCMake"
    VERSION 1.2.0
    DESCRIPTION "CMake C Project Template for Operating Systems II"
    LANGUAGES C
)

#Habilito el testing y lo agrego
include(CTest)

#Defino el estándar de C que se utilizará
set(CMAKE_C_STANDARD 17)

#Defino el directorio de donde se incluirán los archivos de cabecera
include_directories(include)

#Descargo las dependencias
include(FetchContent)

#Defino la URL de donde se tomará la librería Unity
set(UNITY_GIT_URL "https://github.com/ThrowTheSwitch/Unity.git")

#Habilito el debug
set(FETCHCONTENT_QUIET OFF)

FetchContent_Declare(
	Unity
	GIT_REPOSITORY ${UNITY_GIT_URL}
	SOURCE_DIR ${CMAKE_CURRENT_SOURCE_DIR}/external/Unity
	UPDATE_COMMAND ""
)

#Espero hasta que los proyectos estén listos
FetchContent_MakeAvailable(Unity)

#Defino el directorio de donde se tomarán los archivos de código fuente
file(GLOB_RECURSE SOURCES "src/*.c")

#Defino el ejecutable que se generará, con los datos que cargué anteriormente
add_executable(${PROJECT_NAME} ${SOURCES})

#Agrego las subcarpetas que contienen librerías
add_subdirectory(lib/libdyn)
add_subdirectory(lib/libsta)

#Agrego las librerías que se utilizarán
target_include_directories(${PROJECT_NAME} PUBLIC lib/libdyn/include)
target_include_directories(${PROJECT_NAME} PUBLIC lib/libsta/include)

target_link_libraries(${PROJECT_NAME} StatiCLib DynamiCLib)

#Agrego tests
if(RUN_TESTS EQUAL 1 OR RUN_COVERAGE EQUAL 1)
	add_subdirectory(tests)
endif()
