cmake_minimum_required(VERSION 3.1)

project(secp256k1-example LANGUAGES C)

set(SECP256K1_ENABLE_MODULE_RECOVERY ON CACHE BOOL "" FORCE)
set(SECP256K1_BUILD_BENCHMARK OFF CACHE BOOL "" FORCE)
add_subdirectory(src/secp256k1)
target_include_directories(secp256k1 INTERFACE
  $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/src/secp256k1/include>
)
target_include_directories(secp256k1_static INTERFACE
  $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/src/secp256k1/include>
)

add_executable(${PROJECT_NAME} src/ecdsa.c)
target_link_libraries(${PROJECT_NAME} PRIVATE
  secp256k1
  $<$<PLATFORM_ID:Windows>:bcrypt>
)

add_executable(${PROJECT_NAME}-static src/ecdsa.c)
target_link_libraries(${PROJECT_NAME}-static PRIVATE
  secp256k1_static
  $<$<PLATFORM_ID:Windows>:bcrypt>
)

include(GNUInstallDirs)
install(TARGETS ${PROJECT_NAME} ${PROJECT_NAME}-static
  RUNTIME DESTINATION ${CMAKE_INSTALL_BINDIR}
)
