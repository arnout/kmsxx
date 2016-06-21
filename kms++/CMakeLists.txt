include_directories(${LIBDRM_INCLUDE_DIRS})
link_directories(${LIBDRM_LIBRARY_DIRS})

include_directories(${LIBDRM_OMAP_INCLUDE_DIRS})
link_directories(${LIBDRM_OMAP_LIBRARY_DIRS})

file(GLOB SRCS "src/*.cpp" "src/*.h" "inc/kms++/*.h")

if(LIBDRM_OMAP_FOUND)
    file(GLOB OMAP_SRCS "src/omap/*.cpp" "src/omap/*.h" "inc/kms++/omap/*.h")
endif()

add_library(kms++ ${SRCS} ${OMAP_SRCS})

target_include_directories(kms++ PUBLIC
    $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/inc>
    $<INSTALL_INTERFACE:include>
    PRIVATE src)

target_link_libraries(kms++ ${LIBDRM_LIBRARIES} ${LIBDRM_OMAP_LIBRARIES})
