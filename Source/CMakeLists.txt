# ------------------------------------------------------------------------------
#   Copyright (c) Charles Carley.
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


set(FREETYPE_SRC 
  2.10.4/src/autofit/autofit.c
  2.10.4/src/base/ftbase.c
  2.10.4/src/base/ftbbox.c
  2.10.4/src/base/ftbdf.c
  2.10.4/src/base/ftbitmap.c
  2.10.4/src/base/ftcid.c
  2.10.4/src/base/ftfstype.c
  2.10.4/src/base/ftgasp.c
  2.10.4/src/base/ftglyph.c
  2.10.4/src/base/ftgxval.c
  2.10.4/src/base/ftinit.c
  2.10.4/src/base/ftmm.c
  2.10.4/src/base/ftotval.c
  2.10.4/src/base/ftpatent.c
  2.10.4/src/base/ftpfr.c
  2.10.4/src/base/ftstroke.c
  2.10.4/src/base/ftsynth.c
  2.10.4/src/base/fttype1.c
  2.10.4/src/base/ftwinfnt.c
  2.10.4/src/bdf/bdf.c
  2.10.4/src/bzip2/ftbzip2.c
  2.10.4/src/cache/ftcache.c
  2.10.4/src/cff/cff.c
  2.10.4/src/cid/type1cid.c
  2.10.4/src/gzip/ftgzip.c
  2.10.4/src/lzw/ftlzw.c
  2.10.4/src/pcf/pcf.c
  2.10.4/src/pfr/pfr.c
  2.10.4/src/psaux/psaux.c
  2.10.4/src/pshinter/pshinter.c
  2.10.4/src/psnames/psnames.c
  2.10.4/src/raster/raster.c
  2.10.4/src/sfnt/sfnt.c
  2.10.4/src/smooth/smooth.c
  2.10.4/src/truetype/truetype.c
  2.10.4/src/type1/type1.c
  2.10.4/src/type42/type42.c
  2.10.4/src/winfonts/winfnt.c
)

if (WIN32)
	set(FREETYPE_PLATFORM
		2.10.4/src/base/ftdebug.c
		)
	add_definitions(-D_CRT_SECURE_NO_WARNINGS -D_CRT_SECURE_NO_DEPRECATE -D_CRT_NONSTDC_NO_DEPRECATE)
endif (WIN32)

if (APPLE)
	add_definitions(-DDARWIN_NO_CARBON)
endif()


include_directories(2.10.4/include)
add_definitions(-DFT2_BUILD_LIBRARY)
add_library(${TargetName} ${FREETYPE_SRC} ${FREETYPE_PLATFORM})

if (TargetFolders)
    set_target_properties(${TargetName} PROPERTIES FOLDER "${TargetGroup}")
endif()