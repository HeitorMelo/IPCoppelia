cmake_minimum_required(VERSION 3.0.0)
project(IPCoppelia VERSION 0.1.0 LANGUAGES C CXX)

include(CTest)
enable_testing()

add_executable(Bracos bracos.cpp ${CMAKE_CURRENT_SOURCE_DIR}/programming/include/simLib/simConst.h ${CMAKE_CURRENT_SOURCE_DIR}/remoteApi/extApi.h ${CMAKE_CURRENT_SOURCE_DIR}/remoteApi/extApi.c ${CMAKE_CURRENT_SOURCE_DIR}/remoteApi/extApiPlatform.h ${CMAKE_CURRENT_SOURCE_DIR}/remoteApi/extApiPlatform.c)

include(${CMAKE_CURRENT_SOURCE_DIR}/programming/include/cmake/FindCoppeliaSim.cmake)

target_compile_definitions(Bracos PRIVATE NON_MATLAB_PARSING DO_NOT_USE_SHARED_MEMORY MAX_EXT_API_CONNECTIONS=255)

target_include_directories(Bracos PRIVATE ${COPPELIASIM_INCLUDE_DIR})
target_link_libraries(Bracos PRIVATE ${COPPELIASIM_LIBRARIES})
target_include_directories(Bracos PRIVATE ${CMAKE_CURRENT_SOURCE_DIR}/remoteApi)

set(CPACK_PROJECT_NAME ${PROJECT_NAME})
set(CPACK_PROJECT_VERSION ${PROJECT_VERSION})
include(CPack)