add_library(stm32-hal-sht3x sht3x.c sht3x.h)
target_include_directories(stm32-hal-sht3x INTERFACE ${CMAKE_CURRENT_SOURCE_DIR})
