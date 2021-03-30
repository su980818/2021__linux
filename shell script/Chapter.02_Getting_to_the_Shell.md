# In This Chapter


# 1. Accessing the command line

CLI에 접근하는 2가지 방법

#### A.Console Terminals ["CLI terminals “outside the GUI.”"]()

take the Linux system out of graphical desktop mode and place it in text mode.

linux을 시작하면 컴퓨터와 연결된 CLI teminal(tty)위에 GUI를 올림

linux는 시작과 동시에 기본 tty 이외에 다른 선으로 연결된 컴퓨터에도 CLI를 지원하기 위해 virtual tty(tty1~6)을 생성하고 이 virtual tty에 접근 함으로써 CLI를 사용가능. 




#### B.Graphical Terminals ["CLI terminals “in theGUI""]()

use a terminal emulation package from within the Linux graphical desktop environment. 

terminal emulator에 경우도 결국 virtual tty인것은 변함 없음으로 pts(tty7)를 통해 CLI를 제공.

# 2. Reaching CLI via a Linux console terminal
Ctrl+Alt key combination and then press a function key (F1 through F7)
![image](https://user-images.githubusercontent.com/78835559/112934260-5b513700-915c-11eb-82e5-012983adabb5.png)
*# tty3 (Teletypewriter is a old machine used for sending messages) 는 3번 virtual console 에 있음을 보여줌*


###### < setterm Options for Foreground and Background Appearance >

| Option| Parameter Choices |Description|
|-|-|-|
|-background |black, red, green, yellow, blue, magenta, cyan, or white | Changes the terminal’s background color to the one specified|
|-foreground |black, red, green, yellow, blue, magenta, cyan, or white |Changes the terminal’s foreground color, specifically text, to the one specified|
|-inversescreen |on or off | Switches the background color to the foreground color and the foreground color to the background color|
|-reset| None |Changes the terminal appearance back to its default setting and clears the screen|
|-store |None |Sets the current terminal’s foreground and background colors as the values to be used for -reset|
 


# 3. Reaching CLI via a graphical terminal emulator
여러가지 terminal emulator가 있지만 linux에서는 e GNOME Terminal, Konsole Terminal, and xterm 가 일반적

![image](https://user-images.githubusercontent.com/78835559/112936938-b174a900-9161-11eb-8ada-014216773589.png)
*# 여러창을 띠우자 pts0번부터 가상 emulation terminal 이 생성된다.*


##  Using the GNOME terminal emulator
Ctrl+Alt+T 로 시작 
여러가지 편의 기능은 Shitft+Ctrl 을 조합해서 사용되는게 일반적

###### < The File Menu >


|Name |Shortcut Key |Description|
|-|-|-|
|Open Terminal|Shift+Ctrl+N |Starts a new shell session in a new GNOME Terminal window|
|Open Tab| Shift+Ctrl+T |Starts a new shell session in a new tab in the existing GNOME Terminal window|
|New Profile| None |Customizes a session and saves as a profile, which can be recalled for later use |
|Save Contents| None |Saves the scrollback buffer contents to a text file|
|Close Tab |Shift+Ctrl+W |Closes the current tab session|
|Close Window |Shift+Ctrl+Q |Closes the current GNOME Terminal session|

###### < The Edit Menu >
|Name |Shortcut Key |Description|
|-|-|-|
|Copy |Shift+Ctrl+C |Copies selected text to the GNOME clipboard|
|Paste| Shift+Ctrl+V |Pastes text from the GNOME clipboard into a session|
|Paste Filenames ||Properly pastes copied filenames and their paths|
|Select All |None| Selects output in the entire scrollback buffer|
|Profiles| None| Adds, deletes, or modifies GNOME Terminal profiles|
|Keyboard Shortcuts| None| Creates key combinations to quickly access GNOME Terminal features|
|Profile Preferences| None |Edits the current session profile|

###### < The View Menu >
|Name |Shortcut Key| Description|
|-|-|-|
|Show Menubar| None| Toggles on/off the menu bar display|
|Full Screen |F11| Toggles on/off the terminal window filling the entire desktop|
|Zoom In |Ctrl++| Enlarges the font size in the window incrementally|
|Zoom Out |Ctrl+-| Reduces the font size in the window incrementally|
|Normal Size| Ctrl+0| Returns the font size to default|
