---
layout: post
title: clean up qq
description: ""
tags:
comments: true
share: true
date: 2014-03-19 12:10
---

{% highlight bat %}
@echo off

if not exist "Files\" goto:eof

cd/d "%~dp0\Files\Bin"

copy ..\..\QQ\Bin\netapi32.dll .

set DEBUG=

for %%f in (^
    auclt.exe ^
    QQApp.exe ^
    QQPI.exe ^
    QQSafeUD.exe ^
    StorageTool.exe ^
    Tencentdl.exe ^
    Timwp.exe ^
    TXPlatform.exe ^
    maLauncher.exe ^
    maUpdat.exe ^
    QPerfHelper.exe ^
    QScanEngine.dll
) do (

    %DEBUG% ren %%f %%~nf2%%~xf
)

cd..

rd/s/q QQProtect

echo D|xcopy /y /e ..\QQ\Misc\Sound .\Misc\Sound

del QQUninst.exe txupd.exe

cd Plugin

md Disabled

for %%p in (^
    Com.Tencent.Advertisement ^
    Com.Tencent.CRM ^
    Com.Tencent.GameLife ^
    Com.Tencent.Graffito ^
    Com.Tencent.HRTX ^
    Com.Tencent.Memo ^
    Com.Tencent.MMOG ^
    Com.Tencent.NetBar ^
    Com.Tencent.PaiPai ^
    Com.Tencent.PayCenter ^
    Com.Tencent.QQGame ^
    Com.Tencent.QQLive ^
    Com.Tencent.QQMusic ^
    Com.Tencent.QQPet ^
    Com.Tencent.QQRing ^
    Com.Tencent.QQShow ^
    Com.Tencent.QQWebsite ^
    Com.Tencent.QT ^
    Com.Tencent.Soso ^
    Com.Tencent.SpeedDating ^
    Com.Tencent.Stock ^
    Com.Tencent.Today ^
    Com.Tencent.VAS ^
    Com.Tencent.WBlog ^
    Com.Tencent.WenWen ^
    Com.Tencent.Winks
) do (

    rem %DEBUG% rd/s/q %%p
    %DEBUG% move %%p Disabled
)

echo on

:rename

cd/d "%~dp0"
ren QQ QQ2
ren Files QQ
{% endhighlight %}
