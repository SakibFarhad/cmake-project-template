set(SOURCE_FILES  division.cpp)

add_library(division SHARED STATIC ${SOURCE_FILES})

install(TARGETS division DESTINATION ${DIVISIBLE_INSTALL_LIB_DIR})
