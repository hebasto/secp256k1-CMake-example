cmake_minimum_required(VERSION 3.1)

project(secp256k1-example LANGUAGES C)

add_subdirectory(src/secp256k1 EXCLUDE_FROM_ALL)

add_executable(${PROJECT_NAME} src/ecdsa.c)
target_include_directories(${PROJECT_NAME} PRIVATE
  $<BUILD_INTERFACE:${PROJECT_SOURCE_DIR}/src/secp256k1/include>
)
target_link_libraries(${PROJECT_NAME} PRIVATE
  secp256k1
  $<$<PLATFORM_ID:Windows>:bcrypt>
)

add_executable(${PROJECT_NAME}-static src/ecdsa.c)
target_include_directories(${PROJECT_NAME}-static PRIVATE
  $<BUILD_INTERFACE:${PROJECT_SOURCE_DIR}/src/secp256k1/include>
)
target_link_libraries(${PROJECT_NAME}-static PRIVATE
  secp256k1_static
  $<$<PLATFORM_ID:Windows>:bcrypt>
)
