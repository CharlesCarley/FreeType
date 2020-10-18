# -----------------------------------------------------------------------------
#
#   Copyright (c) 2019 Charles Carley.
#
# ------------------------------------------------------------------------------
#   This software is provided 'as-is', without any express or implied
# warranty. In no event will the authors be held liable for any damages
# arising from the use of this software.
#
#   Permission is granted to anyone to use this software for any purpose,
# including commercial applications, and to alter it and redistribute it
# freely, subject to the following restrictions:
#
# 1. The origin of this software must not be misrepresented; you must not
#    claim that you wrote the original software. If you use this software
#    in a product, an acknowledgment in the product documentation would be
#    appreciated but is not required.
# 2. Altered source versions must be plainly marked as such, and must not be
#    misrepresented as being the original software.
# 3. This notice may not be removed or altered from any source distribution.
# ------------------------------------------------------------------------------
if (FreeType_ExternalTarget)
    set(TargetFolders ${FreeType_TargetFolders})
    set(TargetName    ${FreeType_TargetName})
    set(TargetGroup   ${FreeType_TargetGroup})
else()
    set(TargetFolders FALSE)
    set(TargetName    FreeType)
    unset(TargetGroup )
endif()


if (CMAKE_COMPILER_IS_GNUCXX)
	add_definitions(-w)
else()
	add_definitions(/W0)
endif()


set(FREETYPE_SRC 
	src/autofit/autofit.c
	src/bdf/bdf.c
	src/cff/cff.c
	src/base/ftbase.c
	src/base/ftbbox.c
	src/base/ftbdf.c
	src/base/ftbitmap.c
	src/cache/ftcache.c
	src/base/ftgasp.c
	src/base/ftglyph.c
	src/base/ftgxval.c
	src/gzip/ftgzip.c
	src/base/ftinit.c
	src/lzw/ftlzw.c
	src/base/ftmm.c
	src/base/ftotval.c
	src/base/ftpfr.c
	src/base/ftstroke.c
	src/base/ftsynth.c
	src/base/ftsystem.c
	src/base/fttype1.c
	src/base/ftwinfnt.c
	src/base/ftxf86.c
	src/pcf/pcf.c
	src/pfr/pfr.c
	src/psaux/psaux.c
	src/pshinter/pshinter.c
	src/psnames/psmodule.c
	src/raster/raster.c
	src/sfnt/sfnt.c
	src/smooth/smooth.c
	src/truetype/truetype.c
	src/type1/type1.c
	src/cid/type1cid.c
	src/type42/type42.c
	src/winfonts/winfnt.c
)

if (WIN32)
	set(FREETYPE_PLATFORM
		win32/ftdebug.c
		)
endif (WIN32)

if (APPLE)
	add_definitions(-DDARWIN_NO_CARBON)
endif()


include_directories(include)
add_definitions(-DFT2_BUILD_LIBRARY)
add_library(${TargetName} ${FREETYPE_SRC} ${FREETYPE_PLATFORM})

if (TargetFolders)
    set_target_properties(${TargetName} PROPERTIES FOLDER "${TargetGroup}")
endif()