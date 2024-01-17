cmake_minimum_required (VERSION 3.0)
project (SDL2_gfx
    VERSION 2.0.27
    LANGUAGES C
)

find_package (SDL2 REQUIRED)

add_library (${PROJECT_NAME})
add_library ("${PROJECT_NAME}::${PROJECT_NAME}" ALIAS ${PROJECT_NAME})

target_include_directories (
	${PROJECT_NAME} PUBLIC
	${CMAKE_CURRENT_SOURCE_DIR}
)

target_sources (${PROJECT_NAME} PRIVATE
	SDL_framerate.c
	SDL_gfxBlitFunc.c
	SDL_gfxPrimitives.c
	SDL_imageFilter.c
	SDL_rotozoom.c
	)

target_link_libraries (${PROJECT_NAME} PUBLIC
	$<IF:$<BOOL:${BUILD_SHARED_LIBS}>,SDL2::SDL2,SDL2::SDL2-static>
	)

install (TARGETS ${PROJECT_NAME} DESTINATION lib)
install (FILES ${INCLUDE_FILES} DESTINATION include/SDL)
