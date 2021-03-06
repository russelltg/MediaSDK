# Copyright (c) 2018 Intel Corporation
#
# Permission is hereby granted, free of charge, to any person obtaining a copy
# of this software and associated documentation files (the "Software"), to deal
# in the Software without restriction, including without limitation the rights
# to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
# copies of the Software, and to permit persons to whom the Software is
# furnished to do so, subject to the following conditions:
#
# The above copyright notice and this permission notice shall be included in all
# copies or substantial portions of the Software.
#
# THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
# IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
# FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
# AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
# LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
# OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
# SOFTWARE.

if( API_VERSION VERSION_GREATER 1.25 )
    set(MFX_ORIG_LDFLAGS "${MFX_LDFLAGS}" )

    mfx_include_dirs( )

    include_directories( ${CMAKE_CURRENT_SOURCE_DIR}/mctf/include )
    include_directories( ${MSDK_LIB_ROOT}/genx/mctf/include )
    include_directories( ${MSDK_STUDIO_ROOT}/shared/asc/include )

    include_directories( ${MSDK_LIB_ROOT}/cmrt_cross_platform/include )
    include_directories( ${MSDK_STUDIO_ROOT}/shared/include )

    set( sources "" )
    set( sources.plus "" )

    file( GLOB_RECURSE srcs "${CMAKE_CURRENT_SOURCE_DIR}/mctf/src/*.cpp"
                            "${MSDK_LIB_ROOT}/genx/mctf/src/*.cpp"
    )
    list( APPEND sources ${srcs})
    list (REMOVE_ITEM sources "${MSDK_LIB_ROOT}/genx/mctf/src/genx_mc.cpp")
    list (REMOVE_ITEM sources "${MSDK_LIB_ROOT}/genx/mctf/src/genx_me.cpp")
    list (REMOVE_ITEM sources "${MSDK_LIB_ROOT}/genx/mctf/src/genx_sd.cpp")

    make_library( mctf hw static )
    set( defs "" )
endif()
