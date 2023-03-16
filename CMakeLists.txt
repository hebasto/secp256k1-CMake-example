cmake_minimum_required(VERSION 3.1)

project(secp256k1-example LANGUAGES C)

find_package(libsecp256k1 0.3.1 EXACT REQUIRED CONFIG)

add_executable(${PROJECT_NAME} src/ecdsa.c)
target_link_libraries(${PROJECT_NAME} PRIVATE
  libsecp256k1::secp256k1
  $<$<PLATFORM_ID:Windows>:bcrypt>
)

add_executable(${PROJECT_NAME}-static src/ecdsa.c)
target_link_libraries(${PROJECT_NAME}-static PRIVATE
  libsecp256k1::secp256k1_static
  $<$<PLATFORM_ID:Windows>:bcrypt>
)
