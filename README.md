# 问题反馈 🐛
欢迎 [创建 Issue](https://github.com/yingDev/WGestures2-mac-bugs/issues/new) <br>
非 Github 用户? 发送邮件至 [me@yingdev.com](mailto:me@yingdev.com) <br> 或 微博[@Nozama](https://weibo.com/u/2361952611)
我会尽量提供帮助和解决问题. 


# 常用功能实现参考
### 复制文件为路径
WG2 按键序列可以模拟右键点击, 结合延迟时间, 可以容易地实现操作自动化
1. 录入一个不包含轨迹的手势, 比如 `◑A`  (鼠标右键+键盘A)
1. 选择 "按键序列", 编辑代码 `+{MOUSE_RIGHT}{SLEEP 50}aa{ENTER}`. (注意： 两次 a 是因为我的电脑上有 Rar，第二次才会选中 “复制为路径” 菜单项, 根据你的实际情况做出调整）

### 打开文件/程序/网址
WG2 支持 Cmd 脚本 和 Lua 脚本, 都可以用于打开文件/程序等:
* Cmd 脚本实现
```bat
explorer "https://yingdev.com" 
REM 或者打开文件 "C:\Windows\notepad.exe"
```
* Lua 脚本实现
```lua
function wgAction(pos,wid,pid,exe,title,mode)
  WG.Open("https://yingdev.com")
  --或者打开文件 WG.Open("C:\\Windows\\notepad.exe")
end
```

### 调整显示器亮度
WG2 提供了 Lua 接口 `WG.SetBrightness(pos, percent_or_delta, isDelta)`。 注意：并非所有显示其都支持通过软件控制亮度。
* `pos` 点坐标，用于确定 “包含该点的那个显示器”，对于 WG2 而言，基本上就是手势起点坐标
* `percent_or_delta` 是一个数字。如果 `isDelta` 为 true （默认），则表示为亮度增量%，比如 +10 或 -10。反之为 0~100的亮度%.
在 Lua 脚本示例中, 你可以找到以下代码:
```lua
--这段代码使用鼠标手势起点 pos 来决定控制哪个显示器, 然后使亮度增加 5 个百分比。 如果成功，在屏幕上显示调整后的亮度值。
function wgAction(pos,wid,pid,exe,title,mode)
  local result = WG.SetBrightness(pos, 5) --or -5
  if(result >= 0) then
    WG.ShowToast('☀'..result..'%', 1000);
  end
end
```

<br><br>
[YingDev.com](https://www.yingdev.com/projects/wgestures2)
