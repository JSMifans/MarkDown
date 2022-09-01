# 去掉桌面小箭头

```shell
reg add "HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Explorer\Shell Icons" /v 29 /d "%systemroot%\system32\imageres.dll,197" /t reg_sz /f
taskkill /f /im explorer.exe
attrib -s -r -h "%userprofile%\AppData\Local\iconcache.db"
del "%userprofile%\AppData\Local\iconcache.db" /f /q
start explorer
pause

```

>  复制代码，新建文本修改后缀名为 bat

>  以管理员身份运行即可