cmake_minimum_required(VERSION 3.10 FATAL_ERROR)

project(mysql_cpp)

set(TARGET_LIB_NAME "mysqlcpp")
set(TARGET_LIB_TYPE "STATIC")
set(MYSQL_INCLUDE_DIR "C:/Program Files/MySQL/MySQL Server 8.0/include")
set(MYSQL_LIB_DIR "C:/Program Files/MySQL/MySQL Server 8.0/lib")

add_library(${TARGET_LIB_NAME} ${TARGET_LIB_TYPE}
  MySqlCpp.hpp
  MySqlCpp.cpp
  MySqlException.hpp
  MySqlException.cpp
  MySqlPreparedStatement.cpp
  MySqlPreparedStatement.hpp
  InputBinder.hpp
  OutputBinder.hpp
  OutputBinder.cpp
)
set_target_properties(${TARGET_LIB_NAME} PROPERTIES FOLDER "${TARGET_LIB_NAME}")

target_include_directories(${TARGET_LIB_NAME} PUBLIC
  ${MYSQL_INCLUDE_DIR}
)
target_link_directories(${TARGET_LIB_NAME} PUBLIC
  ${MYSQL_LIB_DIR}
)
target_link_libraries(${TARGET_LIB_NAME} PUBLIC
  mysqlclient
)

add_executable(examples examples.cpp)
target_link_directories(examples PUBLIC
  ${MYSQL_LIB_DIR}
)
target_link_libraries(examples PUBLIC
  mysqlcpp
  mysqlclient
)
set_target_properties(examples PROPERTIES FOLDER "examples")