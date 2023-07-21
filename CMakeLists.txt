cmake_minimum_required(VERSION 3.13)

project(secp256k1-example LANGUAGES C)

include(ExternalProject)
ExternalProject_Add(secp256k1
  GIT_REPOSITORY https://github.com/bitcoin-core/secp256k1
  GIT_TAG        c545fdc374964424683d9dac31a828adedabe860
  CMAKE_ARGS
    -DSECP256K1_DISABLE_SHARED=ON
    -DSECP256K1_BUILD_BENCHMARK=OFF
    -DSECP256K1_BUILD_TESTS=OFF
    -DSECP256K1_BUILD_EXHAUSTIVE_TESTS=OFF
    -DSECP256K1_BUILD_CTIME_TESTS=OFF
  INSTALL_COMMAND ""
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
