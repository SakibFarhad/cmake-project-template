add_subdirectory(division)
set(SOURCE_FILES main.cpp)

add_executable(${EXECUTABLE_OUTPUT_NAME} ${SOURCE_FILES})
target_link_libraries(${EXECUTABLE_OUTPUT_NAME} division)
install(TARGETS ${EXECUTABLE_OUTPUT_NAME} DESTINATION ${DIVISIBLE_INSTALL_BIN_DIR})
