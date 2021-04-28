This repository contains my artifacts for the DOJOFIVE Practical Challenge.  This is my solution to Option 3: Simulate All The Things.

My inital thought was to pursue option 4 and produce a Rust Hello World program.  But after following the instructions in the Embedded Rust book and installing
numerous packages, the cross-compiling command "cargo build --target thumbv7m-none-eabi" failed.  It complained that "FLASH" in memory.x was already defined.
But removing that definition resulted in a message that FLASH was not defined.  Time for Plan B.

To reproduce my results you will need to install Renode (https://github.com/renode/renode) and the Nordic nRF52 SDK, and the Seggeer SES IDE.

Renode has emulation capabilities for
the nRF52840 device from Nordic.  The Nordic SDK has a file in the examples folder ...\nRF5_SDK_17.0.2\examples\peripheral\uart\main.c.  This example
initializes UARTE0, printfs a line and waits for a 'q' or 'Q' to be entered from the keyboard.  Backup the existing main.c and copy the one from this repo
over it.

In the SES open the session in 
...\nRF5_SDK_17.0.2\examples\peripheral\uart\pca10056\blank\ses\uart_pca10056.emSession.
This is a project specific to the nRF52840 DK board.  Rebuild this project to get the ELF file ...\nRF5_SDK_17.0.2\examples\peripheral\uart\pca10056\blank\ses\Output\Release\Exe\uart_pca10056.elf
to be executed.

Now copy the .resc file from this repo to the Renode\scripts folder.  Edit that file to point to the location of your ELF file from above.
Start Renode from the command line: "renode dojofile.resc".  One is the controller window and the other simulated Uart0.  Enter "start" to
begin the simulation.  The Uart0 window will output 2 lines and echo characters typed on the keyboard until 'q' is entered.

A screenshot of my results is in the repo for comarison.

QED

