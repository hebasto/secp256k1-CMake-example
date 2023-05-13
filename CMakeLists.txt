cmake_minimum_required(VERSION 3.13)

project(secp256k1-example LANGUAGES C)

set(SECP256K1_DISABLE_SHARED ON)
set(SECP256K1_ENABLE_MODULE_RECOVERY ON)
set(SECP256K1_BUILD_BENCHMARK OFF)
add_subdirectory(src/secp256k1)

add_executable(${PROJECT_NAME} src/ecdsa.c)
target_link_libraries(${PROJECT_NAME}
  secp256k1
  $<$<PLATFORM_ID:Windows>:bcrypt>
)

include(GNUInstallDirs)
install(TARGETS ${PROJECT_NAME}
  RUNTIME DESTINATION ${CMAKE_INSTALL_BINDIR}
)
