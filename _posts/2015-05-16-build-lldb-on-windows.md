---
layout: post
title: Windows 上编译 lldb
description: ""
tags: [逆向]
date: 2015-05-16 03:43
---

先 clone 源码

    git clone http://llvm.org/git/llvm.git

    git clone http://llvm.org/git/clang.git

    git clone http://llvm.org/git/lldb.git

再下载

<http://gnuwin32.sourceforge.net/>

<http://www.swig.org/download.html>

<http://www.cmake.org/download/>

把 [ninja.exe]({{site.url}}/bin/Tools/ninja.exe) 放到 ```cmake\bin``` 下

目录结构如下

    +-- build.bat
    |
    +-- GetGnuWin32
    |
    +-- swigwin-3.0.5
    |
    +-- cmake-3.2.2-win32-x86
    |
    +-- llvm
    |
    `-- tools
        |
        +-- clang
        |
        `-- lldb

CMakeLists.txt 加上下面两句

{% highlight bash %}

set(CMAKE_EXE_LINKER_FLAGS "${CMAKE_EXE_LINKER_FLAGS} /OPT:REF")

set(CMAKE_SHARED_LINKER_FLAGS "${CMAKE_SHARED_LINKER_FLAGS} /OPT:REF")

{% endhighlight %}


build.bat 如下

{% highlight bat %}
@echo off
cd/d "%~dp0"

set PATH=%~dp0GetGnuWin32\bin;%~dp0swigwin-3.0.5;%~dp0cmake-3.2.2-win32-x86\bin;%PATH%

call "C:\Program Files (x86)\Microsoft Visual Studio 12.0\VC\vcvarsall.bat" x86

mkdir release
cd release

cmake -G Ninja "%~dp0llvm" -DCMAKE_BUILD_TYPE=RelWithDebInfo

cmd/k

echo ninja lldb

pause

{% endhighlight %}

配置好后直接执行 ninja lldb 就可以编译了

就这么简单的几个步骤, 非要写个长篇大论, 让我折腾半天

<div markdown="0"><a href="{{ site.url }}/bin/Tools/iOS/debugserver" class="btn btn-success">debugserver-320.2.89</a></div>
