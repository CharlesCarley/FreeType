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
set(FT_VER 2.10.4)

set(FREETYPE_SRC 
  ${FT_VER}/src/autofit/autofit.c
  ${FT_VER}/src/base/ftbase.c
  ${FT_VER}/src/base/ftbbox.c
  ${FT_VER}/src/base/ftbdf.c
  ${FT_VER}/src/base/ftbitmap.c
  ${FT_VER}/src/base/ftcid.c
  ${FT_VER}/src/base/ftfstype.c
  ${FT_VER}/src/base/ftgasp.c
  ${FT_VER}/src/base/ftglyph.c
  ${FT_VER}/src/base/ftgxval.c
  ${FT_VER}/src/base/ftinit.c
  ${FT_VER}/src/base/ftmm.c
  ${FT_VER}/src/base/ftotval.c
  ${FT_VER}/src/base/ftpatent.c
  ${FT_VER}/src/base/ftpfr.c
  ${FT_VER}/src/base/ftstroke.c
  ${FT_VER}/src/base/ftsynth.c
  ${FT_VER}/src/base/fttype1.c
  ${FT_VER}/src/base/ftwinfnt.c
  ${FT_VER}/src/bdf/bdf.c
  ${FT_VER}/src/bzip2/ftbzip2.c
  ${FT_VER}/src/cache/ftcache.c
  ${FT_VER}/src/cff/cff.c
  ${FT_VER}/src/cid/type1cid.c
  ${FT_VER}/src/gzip/ftgzip.c
  ${FT_VER}/src/lzw/ftlzw.c
  ${FT_VER}/src/pcf/pcf.c
  ${FT_VER}/src/pfr/pfr.c
  ${FT_VER}/src/psaux/psaux.c
  ${FT_VER}/src/pshinter/pshinter.c
  ${FT_VER}/src/psnames/psnames.c
  ${FT_VER}/src/raster/raster.c
  ${FT_VER}/src/sfnt/sfnt.c
  ${FT_VER}/src/smooth/smooth.c
  ${FT_VER}/src/truetype/truetype.c
  ${FT_VER}/src/type1/type1.c
  ${FT_VER}/src/type42/type42.c
  ${FT_VER}/src/winfonts/winfnt.c
  ${FT_VER}/src/base/ftsystem.c
)

if (WIN32)
	add_definitions(-D_CRT_SECURE_NO_WARNINGS 
                    -D_CRT_SECURE_NO_DEPRECATE 
                    -D_CRT_NONSTDC_NO_DEPRECATE)
    list(APPEND FREETYPE_SRC ${FT_VER}/builds/windows/ftdebug.c)
else()
    list(APPEND FREETYPE_SRC ${FT_VER}/src/base/ftdebug.c)
endif()

if (APPLE)
	add_definitions(-DDARWIN_NO_CARBON)
endif()


include_directories(${FT_VER}/include)
add_definitions(-DFT2_BUILD_LIBRARY)

add_library(
    ${TargetName} 
    ${FREETYPE_SRC} 
    )

if (TargetFolders)
    set_target_properties(${TargetName} PROPERTIES FOLDER "${TargetGroup}")
endif()