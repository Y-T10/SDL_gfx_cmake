cmake_minimum_required (VERSION 3.0)
project(SDL_gfx
    VERSION 2.0.27
    LANGUAGES C
)

find_package(SDL2 REQUIRED)

include_directories (
	"${SDL2_INCLUDE_DIR}"
	)

add_library (SDL_gfx SHARED)


target_include_directories(
	SDL_gfx PUBLIC
	${CMAKE_CURRENT_SOURCE_DIR}
)

target_sources(SDL_gfx PRIVATE
	SDL_framerate.c
	SDL_gfxBlitFunc.c
	SDL_gfxPrimitives.c
	SDL_imageFilter.c
	SDL_rotozoom.c
	)

target_link_libraries (SDL_gfx PUBLIC
	$<IF:$<BOOL:${BUILD_SHARED_LIBS}>,SDL2::SDL2,SDL2::SDL2-static>
	)

install (TARGETS SDL_gfx DESTINATION lib)
install (FILES ${INCLUDE_FILES} DESTINATION include/SDL)
