cmake_minimum_required(VERSION 3.13)

project(secp256k1-example LANGUAGES C)

include(ExternalProject)
ExternalProject_Add(secp256k1_external
  # INSTALL_DIR hebasto/secp-install
  GIT_REPOSITORY https://github.com/bitcoin-core/secp256k1
  GIT_TAG        c545fdc374964424683d9dac31a828adedabe860
  CMAKE_ARGS
    # -DCMAKE_INSTALL_PREFIX=secp256k1_external
    -DSECP256K1_DISABLE_SHARED=ON
    -DSECP256K1_BUILD_BENCHMARK=OFF
    -DSECP256K1_BUILD_TESTS=OFF
    -DSECP256K1_BUILD_EXHAUSTIVE_TESTS=OFF
    -DSECP256K1_BUILD_CTIME_TESTS=OFF
  INSTALL_COMMAND ""
)
ExternalProject_Get_property(secp256k1_external SOURCE_DIR BINARY_DIR)
add_library(secp256k1 STATIC IMPORTED)
set_target_properties(secp256k1 PROPERTIES
  IMPORTED_LOCATION ${BINARY_DIR}/${CMAKE_STATIC_LIBRARY_PREFIX}secp256k1${CMAKE_STATIC_LIBRARY_SUFFIX}
)
target_include_directories(secp256k1 INTERFACE
  $<BUILD_INTERFACE:${SOURCE_DIR}/include>
)

add_executable(${PROJECT_NAME} src/ecdsa.c)
target_link_libraries(${PROJECT_NAME}
  secp256k1
  $<$<PLATFORM_ID:Windows>:bcrypt>
)

include(GNUInstallDirs)
install(TARGETS ${PROJECT_NAME}
  RUNTIME DESTINATION ${CMAKE_INSTALL_BINDIR}
)
