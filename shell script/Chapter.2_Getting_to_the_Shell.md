# In This Chapter


# 1. Accessing the command line
CLI에 접근하는 2가지 방법
+ Console Terminals ["CLI terminals “outside the GUI.”"]()
take the Linux system out of graphical desktop mode and place it in text mode.
linux을 시작할때 생성되는 6개의 virtual consoles에 엑세스 함으로 동작. 



+ Graphical Terminals ["CLI terminals “in theGUI""]()
use a terminal emulation package from within the Linux graphical desktop environment. 

# 2. Reaching CLI via a Linux console terminal
Ctrl+Alt key combination and then press a function key (F1 through F7)
![image](https://user-images.githubusercontent.com/78835559/112934260-5b513700-915c-11eb-82e5-012983adabb5.png)
*# tty3 (Teletypewriter is a old machine used for sending messages) 는 3번 virtual console 에 있음을 보여줌*


###### <setterm Options for Foreground and Background Appearance>

| Option| Parameter Choices |Description|
|-|-|-|
|-background |black, red, green, yellow, blue, magenta, cyan, or white | Changes the terminal’s background color to the one specified|
|-foreground |black, red, green, yellow, blue, magenta, cyan, or white |Changes the terminal’s foreground color, specifically text, to the one specified|
|-inversescreen |on or off | Switches the background color to the foreground color and the foreground color to the background color|
|-reset| None |Changes the terminal appearance back to its default setting and clears the screen|
|-store |None |Sets the current terminal’s foreground and background colors as the values to be used for -reset|
 


# 3. Reaching CLI via a graphical terminal emulator
여러가지 terminal emulator가 있지만 linux에서는 e GNOME Terminal, Konsole Terminal, and xterm 가 일반적


##  Using the GNOME terminal emulator
Ctrl+Alt+T 로 시작 
여러가지 편의 기능은 Shitft+Ctrl 을 조합해서 사용되는게 일반적

|Name |Shortcut Key |Description|
|-|-|-|
|Open Terminal|Shift+Ctrl+N |Starts a new shell session in a new GNOME Terminal window|
|Open Tab| Shift+Ctrl+T |Starts a new shell session in a new tab in the existing GNOME Terminal window|
|New Profile| None |Customizes a session and saves as a profile, which can be recalled for later use |
|Save Contents| None |Saves the scrollback buffer contents to a text file|
|Close Tab |Shift+Ctrl+W |Closes the current tab session|
|Close Window |Shift+Ctrl+Q |Closes the current GNOME Terminal session|




