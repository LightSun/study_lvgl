cmake_minimum_required(VERSION 3.12.4)
project(lvgl_test LANGUAGES C CXX)
set(CMAKE_INCLUDE_CURRENT_DIR ON)


SET(LVGL_FLAGS "-Wall -Wextra \
    -Wshadow -Wundef -Wmaybe-uninitialized -Wmissing-prototypes -Wno-discarded-qualifiers \
    -Wno-unused-function -Wno-error=strict-prototypes -Wpointer-arith -fno-strict-aliasing -Wno-error=cpp -Wuninitialized \
    -Wno-unused-parameter -Wno-missing-field-initializers -Wno-format-nonliteral -Wno-cast-qual -Wunreachable-code -Wno-switch-default  \
    -Wreturn-type -Wmultichar -Wformat-security -Wno-ignored-qualifiers -Wno-error=pedantic -Wno-sign-compare -Wno-error=missing-prototypes -Wdouble-promotion -Wclobbered -Wdeprecated  \
    -Wempty-body -Wshift-negative-value -Wstack-usage=2048 \
-Wtype-limits -Wsizeof-pointer-memaccess -Wpointer-arith")
set(CMAKE_C_FLAGS "${CMAKE_CXX_FLAGS} ${LVGL_FLAGS}")

include_directories(ui/simulator/inc/)

add_compile_definitions(SIMULATOR=1)
add_compile_definitions(LV_BUILD_TEST=0)

add_subdirectory(lvgl/)
add_subdirectory(lv_drivers/)

add_executable(demo
    main/src/main.c
    main/src/mouse_cursor_icon.c
    )

target_link_libraries(demo PUBLIC
    lv_drivers lvgl lvgl_demos lvgl_examples
    SDL2 m)

