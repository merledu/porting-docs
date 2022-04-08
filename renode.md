# Running TF-Lite Model on RENODE (Litex Vexx RISC-V SoC)

## STEP :01 

GO TO THIS GITHUB LINK: https://github.com/renode/renode
 
## STEP :02 
FROM ABOVE LINK FIRST OF ALL INSTALL THESE BELOW MENTIONED FILES FROM THE RELEASE SECTION :
 1. renode-1.12.0-1-x86_64.pkg.tar.xz8.13 MB
 2. renode-1.12.0-1.f23.x86_64.rpm12.5 MB
 3. renode-1.12.0.linux-portable.tar.gz46.1 MB
 4. renode_1.12.0.dmg14.3 MB
 5. renode_1.12.0.msi15.7 MB
 6. renode_1.12.0.zip15.2 MB
 7. renode_1.12.0_amd64.deb12.6 MB
 8. Source code (zip)
 9. Source code (tar.gz)
 
## STEP:03
UNPACK THESE FILES USING :
```bash
mkdir renode_portable
tar xf  renode-*.linux-portable.tar.gz -C renode_portable --strip-components=1
```

## STEP:04 
TO USE IT FROM ANY LOCATION ENTER THE CREATED DIRECTORY AND ADD IT TO THE SYSTEM PATH:
```bash
cd renode_portable
export PATH="`pwd`:$PATH"
```

## STEP:05
Open terminal and write 
```bash
renode
```
you will see the renode monitor that is CLI. From this CLI window you can create and control the whole emulation environment.

## STEP:06
All the  boards and SoCs are available in the `scripts/singlenode` folder.
To load a script (which in Renode will typically use the .resc extension), use:

```c
include @/path/to/script.resc
```
for example
```c
include @/home/mahnoor/renode/renode_portable/scripts/single-node/litex.resc
```

## STEP:07
IF YOU WANT TO RUN ZEPHYR ON RENODE:

install zephyr from: https://docs.zephyrproject.org/latest/getting_started/index.html

## STEP:08
To build the shell demo application for the LiteX/VexRiscv board run the following commands on Linux .

```bash
cd ~/zephyrproject/zephyr
source zephyr-env.sh
west build -p auto -b litex_vexriscv samples/subsys/shell/shell_module/
```
## STEP:09
Now type `renode` in CLI

## STEP:10
 renode monitor will show , now run the zephyr binary on renode 
 on renode monitor run these below mentioned commands
```bash
(monitor) $zephyr=@/path/to/zephyrproject/zephyr/build/zephyr/zephyr.elf
(monitor) start @scripts/single-node/litex_vexriscv_zephyr.resc
```

E: if you will get an error from the above command;
goto: https://www.mono-project.com/download/stable/

**It looks like mono can't find the libdl.so file. Perhaps it's the .2 postfix in the filename.**

Then Run this command
```bash
sudo ln -s /usr/lib/x86_64-linux-gnu/libdl.so.2 /usr/lib/dl
```

E: if you get an error :
```bash
(monitor) $zephyr?=@/path/to/zephyrproject/zephyr/build/zephyr/zephyr.elf                (zephyr binary)
(monitor) start @scripts/single-node/litex_vexriscv_zephyr.resc                         (soc/board )
```

## STEP:11
If you want to run any application on renode :
like we have tflite application
go to the `hello world` folder in zephyr sample applications
OPEN CMD AND RUN:
```bash
west build -b {board}
 for example :
 west build -b litex_vexriscv
 this command will generate the binary of the application
litex_riscv is the board you can build your application in any zephyr supported board
 open renode then enter this command in renode monitor
 (monitor) $zephyr?=@/path/to/zephyrproject/zephyr/samples/modules/tflite-micro/build/zephyr/zephyr.elf                ( give path of your  applicaton zephyr binary)
(monitor) start @scripts/single-node/litex_vexriscv_zephyr.resc  
```
then the UART will open and show the output of the application.

And Hurrah! Your TF-Lite Application is running on Litex Vexx RISC-V SoC under emulation env on RENODE






