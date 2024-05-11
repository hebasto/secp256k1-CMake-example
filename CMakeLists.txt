cmake_minimum_required(VERSION 3.13..3.29)

project(secp256k1-subtree-intergration-example LANGUAGES C)

set(SECP256K1_DISABLE_SHARED ON)
set(SECP256K1_ENABLE_MODULE_ECDH OFF)
set(SECP256K1_ENABLE_MODULE_RECOVERY ON)
add_subdirectory(src/secp256k1 EXCLUDE_FROM_ALL)

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
