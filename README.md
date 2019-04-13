# LinuxIntegrationWSL
### Effect
![Effect](https://i.imgur.com/DkP1cK5.png)
***
### Windows:
1. Install Linux from Microsoft Store

	![Linux distributions](https://i.imgur.com/wIEhRCu.png)
2. Install [VcXsrv](https://sourceforge.net/projects/vcxsrv/).
3. Run XLaunch, set `Multiple windows` option, **display number to 0**, and save config somewhere you won't delete it.

	![XLaunch window](https://i.imgur.com/PnXCuMh.png)
4. Create `linux.bat` file and move it to `C:/Windows/System32`:
    ```sh
    @echo off
    IF "%~1" == "-i" (
        shift

        set "remainingArgs="
        :getRemainingArgs
        if "%~1" neq "" (
            set ^"remainingArgs=%remainingArgs% %1"
            shift /1
            goto :getRemainingArgs
        )

        bash -c -i "export DISPLAY=:0; export LIBGL_ALWAYS_INDIRECT=1; %remainingArgs%"
    ) ELSE (bash -c -i "export DISPLAY=:0; export LIBGL_ALWAYS_INDIRECT=1; screen -d -m %*")
    ```
    - #### How to use `linux.bat`:
    	If you type `linux -i python` you'll have interactive session in current console.
        
        ![Interactive python window](https://i.imgur.com/1MpxExK.png)
    	
        If you type `linux pcmanfm` window will open by `screen` program, so you can still use Windows' console
        
        ![PCmanFM ran in background](https://i.imgur.com/8HZ6v82.png)
5. Create `background_linux.bat` file and add it to autostart:
    ```sh
    @echo off
    YOUR_CONFIG_FILE.xlaunch
    linux startlxde
    ```
6. Run WSL _(`Win+R`, type `wsl` and enter)_ and do linux steps.

	![run wsl](https://i.imgur.com/dzbmXir.png)

### Linux
1. Run update and upgrade:
    ```sh
    sudo apt update
    sudo apt upgrade
    ```
2. Give our user root privileges
    - Check your username: `whoami`
    - Edit your `/etc/passwd` file
    - Change something like this `USERNAME:x:1000:1001::/home/USERNAME:/bin/bash` to `USERNAME:x:0:0::/home/USERNAME:/bin/bash` (just change these two numbers to 0)
3. Install `lxde` and `screen`:
    ```sh
    sudo apt install lxde screen
    ```
4. Edit `/etc/xdg/lxsession/LXDE/autostart`:
	- Empty the file (or leave screensaver if you want)
	
	![autostart](https://i.imgur.com/mTUhSwR.png)
	- Save file
### You did it :sunglasses:
Now if you type in `cmd` something like `linux xterm`, window of that program will be shown on Windows desktop.

![Xterm](https://i.imgur.com/bYIImlA.png)
