cmake_minimum_required(VERSION 3.13)

project(secp256k1-example LANGUAGES C)

# The libsecp256k1 library uses the SameMinorVersion
# compatibility mode.
find_package(libsecp256k1 0.3 REQUIRED CONFIG)

add_executable(${PROJECT_NAME} src/ecdsa.c)
target_link_libraries(${PROJECT_NAME}
  libsecp256k1::secp256k1
  $<$<PLATFORM_ID:Windows>:bcrypt>
)
