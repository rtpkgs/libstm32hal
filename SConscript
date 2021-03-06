#-*- encoding: utf-8 -*-
#---------------------------------------------------------------------------------
# @File:   Sconscript for package 
# @Author: liu2guang
# @Date:   2018-09-19 18:07:00(v0.1.0) 
# 
# @LICENSE: GPLv3: https://github.com/rtpkgs/buildpkg/blob/master/LICENSE.
#
#---------------------------------------------------------------------------------
import os
from building import * 
Import('RTT_ROOT')
Import('rtconfig')

#---------------------------------------------------------------------------------
# Package configuration
#---------------------------------------------------------------------------------
PKGNAME = "libstm32hal"
VERSION = "v0.2.0"
DEPENDS = ["PKG_USING_LIBSTM32HAL"]

#---------------------------------------------------------------------------------
# Compile the configuration 
#
# SOURCES: Need to compile c and c++ source, auto search when SOURCES is empty
# 
# LOCAL_CPPPATH: Local file path (.h/.c/.cpp)
# LOCAL_CCFLAGS: Local compilation parameter 
# LOCAL_ASFLAGS: Local assembly parameters
# 
# CPPPATH: Global file path (.h/.c/.cpp), auto search when LOCAL_CPPPATH/CPPPATH 
#          is empty # no pass!!!
# CCFLAGS: Global compilation parameter 
# ASFLAGS: Global assembly parameters
#
# CPPDEFINES: Global macro definition
# LOCAL_CPPDEFINES: Local macro definition 
# 
# LIBS: Specify the static library that need to be linked
# LIBPATH: Specify the search directory for the library file (.lib/.a)
#
# LINKFLAGS: Link options
#---------------------------------------------------------------------------------
SOURCES          = [] 

LOCAL_CPPPATH    = [] 
LOCAL_CCFLAGS    = "" 
LOCAL_ASFLAGS    = ""

CPPPATH          = [] 
CCFLAGS          = "" 
ASFLAGS          = ""

CPPDEFINES       = []
LOCAL_CPPDEFINES = []

LIBS             = [] 
LIBPATH          = [] 

LINKFLAGS        = "" 

#---------------------------------------------------------------------------------
# Feature clip configuration, optional 
#---------------------------------------------------------------------------------

#---------------------------------------------------------------------------------
# Compiler platform configuration, optional
#---------------------------------------------------------------------------------
if GetDepend("LIBSTM32HAL_USING_STATIC_LIB") == True: 
    if rtconfig.CROSS_TOOL == "keil" and GetDepend(['SOC_STM32F469NI']) == True: 
        LIBS    += ["libstm32hal_f469_armcc"]
        LIBPATH += [GetCurrentDir() + "/libstm32hal/libstm32hal_f469_armcc"] 
        CPPPATH += [GetCurrentDir() + "/libstm32hal/libstm32hal_f469_armcc"] 
    elif rtconfig.CROSS_TOOL == "gcc" and GetDepend(['SOC_STM32F469NI']) == True: 
        LIBS    += ["stm32hal_f469_gcc"]
        LIBPATH += [GetCurrentDir() + "/libstm32hal/libstm32hal_f469_gcc"] 
        CPPPATH += [GetCurrentDir() + "/libstm32hal/libstm32hal_f469_gcc"] 
    else: 
        print("not support cross tool or soc!")
else:
    SOURCES += Glob('libstm32hal/libstm32hal_f4xx/*.c')
    CPPPATH += [GetCurrentDir() + "/libstm32hal/libstm32hal_f4xx"] 

#---------------------------------------------------------------------------------
# Warning: internal related processing, developers do not modify!!! 
#---------------------------------------------------------------------------------

#---------------------------------------------------------------------------------
# System variables
#---------------------------------------------------------------------------------
objs   = [] 
root   = GetCurrentDir() 

#---------------------------------------------------------------------------------
# Sub target
#---------------------------------------------------------------------------------
list = os.listdir(root)
if GetDepend(DEPENDS):
    for d in list:
        path = os.path.join(root, d)
        if os.path.isfile(os.path.join(path, 'SConscript')):
            objs = objs + SConscript(os.path.join(d, 'SConscript')) 

#---------------------------------------------------------------------------------
# Main target
#---------------------------------------------------------------------------------
objs = DefineGroup(name = PKGNAME + '-' + VERSION, src = SOURCES, depend = DEPENDS, 
                   CPPPATH          = CPPPATH, 
                   CCFLAGS          = CCFLAGS, 
                   ASFLAGS          = ASFLAGS, 
                   LOCAL_CPPPATH    = LOCAL_CPPPATH, 
                   LOCAL_CCFLAGS    = LOCAL_CCFLAGS, 
                   LOCAL_ASFLAGS    = LOCAL_ASFLAGS, 
                   CPPDEFINES       = CPPDEFINES, 
                   LOCAL_CPPDEFINES = LOCAL_CPPDEFINES, 
                   LIBS             = LIBS, 
                   LIBPATH          = LIBPATH,
                   LINKFLAGS        = LINKFLAGS)  

Return("objs") 
#---------------------------------------------------------------------------------
# End
#---------------------------------------------------------------------------------
