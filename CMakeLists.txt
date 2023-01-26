cmake_minimum_required(VERSION 3.1)

project(secp256k1-example LANGUAGES C)

find_package(secp256k1 0.2.1 EXACT REQUIRED CONFIG)

add_executable(${PROJECT_NAME} src/ecdsa.c)
target_link_libraries(${PROJECT_NAME} PRIVATE
  secp256k1::secp256k1
  $<$<PLATFORM_ID:Windows>:bcrypt>
)
