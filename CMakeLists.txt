cmake_minimum_required(VERSION 3.14..3.29)

project(secp256k1-fetchcontent-integration-example LANGUAGES C)

set(SECP256K1_DISABLE_SHARED ON CACHE INTERNAL "")
set(SECP256K1_BUILD_BENCHMARK OFF CACHE INTERNAL "")
set(SECP256K1_BUILD_TESTS OFF CACHE INTERNAL "")
set(SECP256K1_BUILD_EXHAUSTIVE_TESTS OFF CACHE INTERNAL "")
set(SECP256K1_BUILD_CTIME_TESTS OFF CACHE INTERNAL "")

include(FetchContent)
FetchContent_Declare(libsecp256k1
  GIT_REPOSITORY https://github.com/bitcoin-core/secp256k1
  # v0.5.0
  GIT_TAG e3a885d42a7800c1ccebad94ad1e2b82c4df5c65
)
FetchContent_MakeAvailable(libsecp256k1)

add_executable(example src/ecdsa.c)
target_link_libraries(example
  PRIVATE
    secp256k1
    $<$<PLATFORM_ID:Windows>:bcrypt>
)

include(GNUInstallDirs)
install(TARGETS example
  RUNTIME DESTINATION ${CMAKE_INSTALL_BINDIR}
)
