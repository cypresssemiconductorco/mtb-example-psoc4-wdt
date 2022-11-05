# PSoC&trade; 4: Watchdog timer interrupt and reset

This code example deals with the watchdog timer (WDT) of PSoC&trade; 4. The watchdog timer operates in two modes: the interrupt mode and the reset mode. In the interrupt mode, the LED toggles every second. When configured in the reset mode, the LED blinks thrice every 4.915 seconds with an interval of 500 milliseconds due to the watchdog resets. In idle mode, the system enters deep sleep mode to save power.

All the intervals used in this code example are configurable.

[View this README on GitHub.](https://github.com/Infineon/mtb-example-psoc4-wdt)

[Provide feedback on this code example.](https://cypress.co1.qualtrics.com/jfe/form/SV_1NTns53sK2yiljn?Q_EED=eyJVbmlxdWUgRG9jIElkIjoiQ0UyMzA2NTMiLCJTcGVjIE51bWJlciI6IjAwMi0zMDY1MyIsIkRvYyBUaXRsZSI6IlBTb0MmdHJhZGU7IDQ6IFdhdGNoZG9nIHRpbWVyIGludGVycnVwdCBhbmQgcmVzZXQiLCJyaWQiOiJib29wYWxhbXNyaW4iLCJEb2MgdmVyc2lvbiI6IjIuMC4wIiwiRG9jIExhbmd1YWdlIjoiRW5nbGlzaCIsIkRvYyBEaXZpc2lvbiI6Ik1DRCIsIkRvYyBCVSI6IklDVyIsIkRvYyBGYW1pbHkiOiJQU09DIn0=)

## Requirements

- [ModusToolbox&trade; software](https://www.infineon.com/modustoolbox) v3.0 or later (tested with v3.0)

  **Note:** This code example version requires ModusToolbox&trade; software version 3.0 or later and is not backward compatible with v2.4 or older versions.

- Board support package (BSP) minimum required version: 3.0.0
- Programming language: C
- Associated parts: [PSoC&trade; 4000S, PSoC&trade; 4100S, PSoC&trade; 4100S Plus, PSoC&trade; 4500S, and PSoC&trade; 4100S Max](https://www.infineon.com/cms/en/product/microcontroller/32-bit-psoc-arm-cortex-microcontroller/psoc-4-32-bit-arm-cortex-m0-mcu/)

## Supported toolchains (make variable 'TOOLCHAIN')

- GNU Arm&reg; embedded compiler v10.3.1 (`GCC_ARM`) - Default value of `TOOLCHAIN`
- Arm&reg; compiler v6.16 (`ARM`)
- IAR C/C++ compiler v9.30.1 (`IAR`)

## Supported kits (make variable 'TARGET')

- [PSoC&trade; 4100S Max pioneer kit](https://www.infineon.com/CY8CKIT-041S-MAX) (`CY8CKIT-041S-MAX`) - Default value of `TARGET`
- [PSoC&trade; 4000S CAPSENSE&trade; prototyping kit](https://www.infineon.com/CY8CKIT-145-40XX) (`CY8CKIT-145-40XX`)
- [PSoC&trade; 4100S Plus prototyping kit](https://www.infineon.com/CY8CKIT-149) (`CY8CKIT-149`)
- [PSoC&trade; 4100S CAPSENSE&trade; pioneer kit](https://www.infineon.com/CY8CKIT-041-41XX) (`CY8CKIT-041-41XX`)
- [PSoC&trade; 4500S pioneer kit](https://www.infineon.com/CY8CKIT-045S) (`CY8CKIT-045S`)


## Hardware setup

This example uses the board's default configuration. See the kit user guide to ensure that the board is configured correctly.

**Note:** The PSoC&trade; 4 kits ship with KitProg2 installed. The ModusToolbox&trade; software requires KitProg3. Before using this code example, make sure that the board is upgraded to KitProg3. The tool and instructions are available in the [Firmware Loader](https://github.com/Infineon/Firmware-loader) GitHub repository. If you do not upgrade, you will see an error like "unable to find CMSIS-DAP device" or "KitProg firmware is out of date".


## Software setup

This example requires no additional software or tools.

## Using the code example

Create the project and open it using one of the following:

<details><summary><b>In Eclipse IDE for ModusToolbox&trade; software</b></summary>

1. Click the **New Application** link in the **Quick Panel** (or, use **File** > **New** > **ModusToolbox&trade; Application**). This launches the [Project Creator](https://www.infineon.com/ModusToolboxProjectCreator) tool.

2. Pick a kit supported by the code example from the list shown in the **Project Creator - Choose Board Support Package (BSP)** dialog.

   When you select a supported kit, the example is reconfigured automatically to work with the kit. To work with a different supported kit later, use the [Library Manager](https://www.infineon.com/ModusToolboxLibraryManager) to choose the BSP for the supported kit. You can use the Library Manager to select or update the BSP and firmware libraries used in this application. To access the Library Manager, click the link from the **Quick Panel**.

   You can also just start the application creation process again and select a different kit.

   If you want to use the application for a kit not listed here, you may need to update the source files. If the kit does not have the required resources, the application may not work.

3. In the **Project Creator - Select Application** dialog, choose the example by enabling the checkbox.

4. (Optional) Change the suggested **New Application Name**.

5. The **Application(s) Root Path** defaults to the Eclipse workspace which is usually the desired location for the application. If you want to store the application in a different location, you can change the *Application(s) Root Path* value. Applications that share libraries should be in the same root path.

6. Click **Create** to complete the application creation process.

For more details, see the [Eclipse IDE for ModusToolbox&trade; software user guide](https://www.infineon.com/MTBEclipseIDEUserGuide) (locally available at *{ModusToolbox&trade; software install directory}/docs_{version}/mt_ide_user_guide.pdf*).

</details>

<details><summary><b>In command-line interface (CLI)</b></summary>

ModusToolbox&trade; software provides the Project Creator as both a GUI tool and the command line tool, "project-creator-cli". The CLI tool can be used to create applications from a CLI terminal or from within batch files or shell scripts. This tool is available in the *{ModusToolbox&trade; software install directory}/tools_{version}/project-creator/* directory.

Use a CLI terminal to invoke the "project-creator-cli" tool. On Windows, use the command line "modus-shell" program provided in the ModusToolbox&trade; software installation instead of a standard Windows command-line application. This shell provides access to all ModusToolbox&trade; software tools. You can access it by typing `modus-shell` in the search box in the Windows menu. In Linux and macOS, you can use any terminal application.

This tool has the following arguments:

Argument | Description | Required/optional
---------|-------------|-----------
`--board-id` | Defined in the `<id>` field of the [BSP](https://github.com/Infineon?q=bsp-manifest&type=&language=&sort=) manifest | Required
`--app-id`   | Defined in the `<id>` field of the [CE](https://github.com/Infineon?q=ce-manifest&type=&language=&sort=) manifest | Required
`--target-dir`| Specify the directory in which the application is to be created if you prefer not to use the default current working directory | Optional
`--user-app-name`| Specify the name of the application if you prefer to have a name other than the example's default name | Optional

<br />

The following example clones the "[mtb-example-psoc4-wdt](https://github.com/Infineon/mtb-example-psoc4-wdt)" application with the desired name "Psoc4Wdt" configured for the *CY8CKIT-149* BSP into the specified working directory, *C:/mtb_projects*:

   ```
   project-creator-cli --board-id CY8CKIT-149 --app-id mtb-example-psoc4-wdt --user-app-name Psoc4Wdt --target-dir "C:/mtb_projects"
   ```

**Note:** The project-creator-cli tool uses the `git clone` and `make getlibs` commands to fetch the repository and import the required libraries. For details, see the "Project creator tools" section of the [ModusToolbox&trade; software user guide](https://www.infineon.com/ModusToolboxUserGuide) (locally available at *{ModusToolbox&trade; software install directory}/docs_{version}/mtb_user_guide.pdf*).

To work with a different supported kit later, use the [Library Manager](https://www.infineon.com/ModusToolboxLibraryManager) to choose the BSP for the supported kit. You can invoke the Library Manager GUI tool from the terminal using `make library-manager` command or use the Library Manager CLI tool "library-manager-cli" to change the BSP.

The "library-manager-cli" tool has the following arguments:

Argument | Description | Required/optional
---------|-------------|-----------
`--add-bsp-name` | Name of the BSP that should be added to the application | Required
`--set-active-bsp` | Name of the BSP that should be as active BSP for the application | Required
`--add-bsp-version`| Specify the version of the BSP that should be added to the application if you do not wish to use the latest from manifest | Optional
`--add-bsp-location`| Specify the location of the BSP (local/shared) if you prefer to add the BSP in a shared path | Optional

<br />

Following example adds the CY8CKIT-041S-MAX BSP to the already created application and makes it the active BSP for the app:

   ```
   library-manager-cli --project "C:/mtb_projects/Psoc4Wdt" --add-bsp-name CY8CKIT-041S-MAX --add-bsp-version "latest-v3.X" --add-bsp-location "local"

   library-manager-cli --project "C:/mtb_projects/Psoc4Wdt" --set-active-bsp APP_CY8CKIT-041S-MAX
   ```

</details>

<details><summary><b>In third-party IDEs</b></summary>

Use one of the following options:

- **Use the standalone [Project Creator](https://www.infineon.com/ModusToolboxProjectCreator) tool:**

   1. Launch Project Creator from the Windows Start menu or from *{ModusToolbox&trade; software install directory}/tools_{version}/project-creator/project-creator.exe*.

   2. In the initial **Choose Board Support Package** screen, select the BSP, and click **Next**.

   3. In the **Select Application** screen, select the appropriate IDE from the **Target IDE** drop-down menu.

   4. Click **Create** and follow the instructions printed in the bottom pane to import or open the exported project in the respective IDE.

<br />

- **Use command-line interface (CLI):**

   1. Follow the instructions from the **In command-line interface (CLI)** section to create the application.

   2. Export the application to a supported IDE using the `make <ide>` command.

   3. Follow the instructions displayed in the terminal to create or import the application as an IDE project.

For a list of supported IDEs and more details, see the "Exporting to IDEs" section of the [ModusToolbox&trade; software user guide](https://www.infineon.com/ModusToolboxUserGuide) (locally available at *{ModusToolbox&trade; software install directory}/docs_{version}/mtb_user_guide.pdf*).

</details>


## Operation

1. Connect the board to your PC using the provided USB cable through the KitProg3 USB connector.

2. By default, the code example works in WDT interrupt mode because the macro `WDT_DEMO` in main.c is set as `WDT_INTERRUPT_DEMO`. To make the WDT work in the reset mode, set the `WDT_DEMO` macro to `WDT_RESET_DEMO` in *main.c* as Figure 1 shows.

   **Figure 1. Accessing WDT operation modes**

   ![](images/modes.png)


3. Program the board using one of the following:

   <details><summary><b>Using Eclipse IDE for ModusToolbox&trade; software</b></summary>

      1. Select the application project in the Project Explorer.

      2. In the **Quick Panel**, scroll down, and click **\<Application Name> Program (KitProg3_MiniProg4)**.
   </details>

   <details><summary><b>Using CLI</b></summary>

     From the terminal, execute the `make program` command to build and program the application using the default toolchain to the default target. The default toolchain is specified in the application's Makefile but you can override this value manually:
      ```
      make program TOOLCHAIN=<toolchain>
      ```

      Example:
      ```
      make program TOOLCHAIN=GCC_ARM
      ```
   </details>

4. Observe the status of LED based on different events summarized as follows:

**Table 1. LED status based on the macro `WDT_DEMO`**

 Project setting  |  LED status
 :------- | :------------
 `WDT_DEMO` set to `WDT_INTERRUPT_DEMO` | LED toggles on every WDT interrupt (interval of 1 s).
 `WDT_DEMO` set to `WDT_RESET_DEMO` with the blocking function   | After approximately 5 s, the device resets and the LED blinks thrice with a 500-ms interval to indicate a WDT reset.

The LED blinks once on a power cycle or an external reset event.

**Note:** The LED states are inverted for the CY8CKIT-149 kit. Macros `LED_STATE_ON` and `LED_STATE_OFF` have to be updated in main.c.

## Debugging

You can debug the example to step through the code. In the IDE, use the **\<Application Name> Debug (KitProg3_MiniProg4)** configuration in the **Quick Panel**. For details, see the "Program and debug" section in the [Eclipse IDE for ModusToolbox&trade; software user guide](https://www.infineon.com/MTBEclipseIDEUserGuide).

## Design and implementation

The WDT in PSoC&trade; 4 is a 16-bit timer and uses the internal low-speed oscillator (ILO) clock of 40-kHz as a source.
The accuracy of ILO is (- 50% to +100%). Therefore, the match value of WDT is set after compensating the ILO with IMO.
The firmware flow is as follows:

1. Set the 'ignore' bits for the WDT counter. In this project, it is set to '0'. This means that the counter works with full 16-bit resolution. This gives an interval of 1.6384 s (65536 ÷ 40 kHz) for the complete count. See the device architecture [TRM](https://www.infineon.com/dgdl/Infineon-PSoC_4100S_and_PSoC_4100S_Plus_PSoC_4_Architecture_TRM-AdditionalTechnicalInformation-v12_00-EN.pdf?fileId=8ac78c8c7d0d8da4017d0f9433460188) Chapter 13. "Watchdog Timer" for more information.

2. Clear the pending WDT interrupt.

3. Enable the ILO, which is the source for the WDT. Start ILO measurement and get the value of `ilo_compensated_counts` that requires to be set after every interrupt match.

4. Write the match value. The WDT can generate an interrupt when the WDT counter reaches the match count. The match count is generated using `DESIRED_WDT_INTERVAL`.

5. For the interrupt mode, enable interrupt generation and assign the interrupt service routine(`wdt_isr`).

6. Enable the WDT.

7. Because the ILO has low accuracy, the `ilo_compensated_counts` are calculated and the match value of the WDT is updated following a WDT interrupt.

8.    The System is put into Deep Sleep in idle mode to save power. Because the watchdog timer works on a low-frequency clock (LFCLK), its operation will not be effected when the system is put into Deep Sleep mode. The watchdog timer interrupt will wake the device from Deep Sleep mode.


**Notes:**

1. In interrupt mode, the WDT is configured to generate interrupts at `WDT_INTERRUPT_INTERVAL_MS` intervals. The default value of `WDT_INTERRUPT_INTERVAL_MS` is 1000 milliseconds. The WDT generates an interrupt on reaching the match value. The WDT counter is not reset on match; it continues to count across the full 16-bit resolution. Therefore, the new match value of the WDT counter is generated and updated on every WDT interrupt event to generate an interrupt after one second from the present interrupt. The WDT interrupt flag is set inside the WDT interrupt service routine; it is checked in the main loop and the LED on the kit is toggled.

2. In reset mode, the WDT is enabled without configuring the ISR and interrupt interval. To demonstrate WDT reset, a blocking code `(while(1))` is present in the innermost `for` loop, which is enabled when `WDT_DEMO` is selected as `WDT_RESET_DEMO`. The firmware must clear the WDT interrupt before the third match event/interrupt. For normal applications, `Cy_WDT_ClearInterrupt()` should be called to clear the WDT interrupt before the timeout (3 * WDT counter time period) is reached. However, when `WDT_DEMO` is set as `WDT_RESET_DEMO`, the firmware will not clear the interrupt. Therefore, the WDT interrupt is not served, which leads to a device reset on the third interrupt.  The default reset interval is 4.915 seconds (= 3 * 1.685). It can be reduced by increasing the value of ignore bits in the `IGNORE_BITS` macro.

3. Because the ILO has low accuracy (-50% to +100%), `ilo_compensated_counts` needs to be periodically calculated using the IMO (+/- 2%).

4. Upon every device reset, the firmware checks whether the reset event is caused by the WDT. If a reset event occurred due to the WDT, the LED blinks thrice with an interval of `DELAY_IN_MS`. If not, it will blink once with the interval of `DELAY_IN_MS`.

5. You can configure the values of the WDT interrupt interval, LED Blink interval, WDT interrupt priority, and a number of ignore bits using macros in *main.c* as shown in Figure 2 and update them.

   **Figure 2. Accessing macros**

   ![Figure 2](images/macros.png)

### Resources and settings

**Table 2. Application resources**

 Resource  |  Alias/object     |    Purpose
 :------- | :------------    | :------------
 WDT (PDL) | -          | WDT driver to configure the hardware resource
 GPIO (PDL)    | CYBSP_USER_LED         | LED

<br>

## Related resources

Resources  | Links
-----------|----------------------------------
Application notes  | [AN79953](https://www.infineon.com/AN79953) – Getting started with PSoC&trade; 4
Code examples  | [Using ModusToolbox&trade; software](https://github.com/Infineon/Code-Examples-for-ModusToolbox-Software) on GitHub <br> [Using PSoC&trade; Creator](https://www.infineon.com/cms/en/design-support/software/code-examples/psoc-3-4-5-code-examples-for-psoc-creator/)
Device documentation | Download datasheets, TRMs, and more from the [PSoC&trade; 4 product page](https://www.infineon.com/cms/en/product/microcontroller/32-bit-psoc-arm-cortex-microcontroller/psoc-4-32-bit-arm-cortex-m0-mcu/) <br>
Development kits | Select your kits from the [Evaluation Board Finder](https://www.infineon.com/cms/en/design-support/finder-selection-tools/product-finder/evaluation-board) page.
Libraries on GitHub | [mtb-pdl-cat2](https://github.com/Infineon/mtb-pdl-cat2) – PSoC&trade; 4 peripheral driver library (PDL)<br> [mtb-hal-cat2](https://github.com/Infineon/mtb-hal-cat2) – Hardware abstraction layer (HAL) library
Tools  | [ModusToolbox&trade; software](https://www.infineon.com/modustoolbox) – ModusToolbox&trade; software is a collection of easy-to-use software and tools enabling rapid development with Infineon MCUs, covering applications from embedded sense and control to wireless and cloud-connected systems using AIROC&trade; Wi-Fi and Bluetooth® connectivity devices. <br /> [PSoC&trade; Creator](https://www.infineon.com/cms/en/design-support/tools/sdk/psoc-software/psoc-creator/) – IDE for PSoC&trade; and FM0+ MCU development

<br />

## Other resources

Infineon provides a wealth of data at www.infineon.com to help you select the right device, and quickly and effectively integrate it into your design.

## Document history

Document title: *CE230653* - *PSoC&trade; 4: Watchdog timer interrupt and reset*

 Version | Description of change
 ------- | ---------------------
 1.0.0   | New code example. <br />  This version is not backward compatible with ModusToolbox&trade; software v2.1.
 1.1.0   | Added support for new kits
 2.0.0   | Major update to support ModusToolbox&trade; v3.0. <br> This version is not backward compatible with previous versions of ModusToolbox&trade; software.

<br />

---------------------------------------------------------

© Cypress Semiconductor Corporation, 2020-2022. This document is the property of Cypress Semiconductor Corporation, an Infineon Technologies company, and its affiliates ("Cypress").  This document, including any software or firmware included or referenced in this document ("Software"), is owned by Cypress under the intellectual property laws and treaties of the United States and other countries worldwide.  Cypress reserves all rights under such laws and treaties and does not, except as specifically stated in this paragraph, grant any license under its patents, copyrights, trademarks, or other intellectual property rights.  If the Software is not accompanied by a license agreement and you do not otherwise have a written agreement with Cypress governing the use of the Software, then Cypress hereby grants you a personal, non-exclusive, nontransferable license (without the right to sublicense) (1) under its copyright rights in the Software (a) for Software provided in source code form, to modify and reproduce the Software solely for use with Cypress hardware products, only internally within your organization, and (b) to distribute the Software in binary code form externally to end users (either directly or indirectly through resellers and distributors), solely for use on Cypress hardware product units, and (2) under those claims of Cypress’s patents that are infringed by the Software (as provided by Cypress, unmodified) to make, use, distribute, and import the Software solely for use with Cypress hardware products.  Any other use, reproduction, modification, translation, or compilation of the Software is prohibited.
<br />
TO THE EXTENT PERMITTED BY APPLICABLE LAW, CYPRESS MAKES NO WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, WITH REGARD TO THIS DOCUMENT OR ANY SOFTWARE OR ACCOMPANYING HARDWARE, INCLUDING, BUT NOT LIMITED TO, THE IMPLIED WARRANTIES OF MERCHANTABILITY AND FITNESS FOR A PARTICULAR PURPOSE.  No computing device can be absolutely secure.  Therefore, despite security measures implemented in Cypress hardware or software products, Cypress shall have no liability arising out of any security breach, such as unauthorized access to or use of a Cypress product. CYPRESS DOES NOT REPRESENT, WARRANT, OR GUARANTEE THAT CYPRESS PRODUCTS, OR SYSTEMS CREATED USING CYPRESS PRODUCTS, WILL BE FREE FROM CORRUPTION, ATTACK, VIRUSES, INTERFERENCE, HACKING, DATA LOSS OR THEFT, OR OTHER SECURITY INTRUSION (collectively, "Security Breach").  Cypress disclaims any liability relating to any Security Breach, and you shall and hereby do release Cypress from any claim, damage, or other liability arising from any Security Breach.  In addition, the products described in these materials may contain design defects or errors known as errata which may cause the product to deviate from published specifications. To the extent permitted by applicable law, Cypress reserves the right to make changes to this document without further notice. Cypress does not assume any liability arising out of the application or use of any product or circuit described in this document. Any information provided in this document, including any sample design information or programming code, is provided only for reference purposes.  It is the responsibility of the user of this document to properly design, program, and test the functionality and safety of any application made of this information and any resulting product.  "High-Risk Device" means any device or system whose failure could cause personal injury, death, or property damage.  Examples of High-Risk Devices are weapons, nuclear installations, surgical implants, and other medical devices.  "Critical Component" means any component of a High-Risk Device whose failure to perform can be reasonably expected to cause, directly or indirectly, the failure of the High-Risk Device, or to affect its safety or effectiveness.  Cypress is not liable, in whole or in part, and you shall and hereby do release Cypress from any claim, damage, or other liability arising from any use of a Cypress product as a Critical Component in a High-Risk Device. You shall indemnify and hold Cypress, including its affiliates, and its directors, officers, employees, agents, distributors, and assigns harmless from and against all claims, costs, damages, and expenses, arising out of any claim, including claims for product liability, personal injury or death, or property damage arising from any use of a Cypress product as a Critical Component in a High-Risk Device. Cypress products are not intended or authorized for use as a Critical Component in any High-Risk Device except to the limited extent that (i) Cypress’s published data sheet for the product explicitly states Cypress has qualified the product for use in a specific High-Risk Device, or (ii) Cypress has given you advance written authorization to use the product as a Critical Component in the specific High-Risk Device and you have signed a separate indemnification agreement.
<br />
Cypress, the Cypress logo, and combinations thereof, WICED, ModusToolbox, PSoC, CapSense, EZ-USB, F-RAM, and Traveo are trademarks or registered trademarks of Cypress or a subsidiary of Cypress in the United States or in other countries. For a more complete list of Cypress trademarks, visit cypress.com. Other names and brands may be claimed as property of their respective owners.
