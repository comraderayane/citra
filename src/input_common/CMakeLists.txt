set(SRCS
            analog_from_button.cpp
            keyboard.cpp
            main.cpp
            )

set(HEADERS
            analog_from_button.h
            keyboard.h
            main.h
            )

if(SDL2_FOUND)
    set(SRCS ${SRCS} sdl/sdl.cpp)
    set(HEADERS ${HEADERS} sdl/sdl.h)
    include_directories(${SDL2_INCLUDE_DIR})
endif()

create_directory_groups(${SRCS} ${HEADERS})

add_library(input_common STATIC ${SRCS} ${HEADERS})
target_link_libraries(input_common common core)

if(SDL2_FOUND)
    target_link_libraries(input_common ${SDL2_LIBRARY})
    set_property(TARGET input_common APPEND PROPERTY COMPILE_DEFINITIONS HAVE_SDL2)
endif()
