# **Macropad Hardware Guide**

## **Introduction**
Your macropad is a compact, chain-linkable input device featuring:
-   **6 mechanical keys**
-   **1 onboard RGB LED**
-   **Configurable operating modes** (Master / Node)
-   **Optional integration with the Media Controller**
-   **Expandable multi-pad topology**
    

This guide outlines the hardware layout, how to chain multiple pads, how to assign roles, and how to configure indicators such as RGB lighting.  

For command-level details, refer to the **[Macropad Command Set](https://github.com/respawnin/screendget38-docs/blob/main/README.md)** .

----------

## **Combination Guide**

<img src="https://github.com/respawnin/screendget38-docs/blob/main/imgs/screendget-combi.png?raw=true" alt="screendget38 macropad combination" width="50%" height="50%">

### **Modular Expansion Architecture**

Your macropad units—and the optional media controller—are designed to operate in a **left-to-right daisy chain**
-   The **left-most device** is always the **Master**.  
    This is the one you plug into your computer with **USB-C**.
-   Every device to the **right** of the master must be set as a **Node**.
-   The system supports:
    -   A **Master Macropad** controlling additional macropads (Node units)
    -   A **Master Media Controller** controlling macropads
    -   A **mixed chain** (e.g., Media Controller → Macropad → Macropad)
        
### **Assigning Master / Node Modes**

Each unit must be configured individually. Configure them **one at a time** over USB to avoid addressing conflicts.

 1. Connect the unit directly via USB-C.
 2.  Open the [CLI](https://www.retropy.io/screendget/cli/) (or your WebSerial configurator).
 3.  Enter:
    -   `setmaster` — assigns the device as **Master**
    -   `setnode` — assigns the device as **Node**
        
4.  Disconnect and repeat for each additional unit.

### **Example Configuration**


Suppose you have
 - 1 × Macropad
 - 1 × Media Controller    
 - 1 × Additional Macropad

Your physical order and role assignment might look like:

**[Master: Media Controller] → [Node: Macropad] → [Node: Macropad]**
| CONFIG 1| MASTER                              | NODE|
|---------------|--------------------------------------------|---------|
| |<div align="center"><img src="https://github.com/respawnin/screendget38-docs/blob/main/imgs/usb-c.png?raw=true" alt="usb-c connection" width="30%" height="auto"></div>|
| |<div align="center"><img src="https://github.com/respawnin/screendget38-docs/blob/main/imgs/screendget-media-controller.png?raw=true" alt="media controller" width="70%" height="auto"></div> | <div align="center"><img src="https://github.com/respawnin/screendget38-docs/blob/main/imgs/screendget-macropad.png?raw=true" alt="macropad" width="70%" height="auto"></div>|
| | Assign media controller as master using `setmaster`  | Assign macropad as node using `setnode`|




Or, if you prefer the macropad as the primary controller:

**[Master: Macropad] → [Node: Media Controller] → [Node: Macropad]**
| CONFIG 2| MASTER                              | NODE|
|---------------|--------------------------------------------|---------|
| | <div align="center"><img src="https://github.com/respawnin/screendget38-docs/blob/main/imgs/usb-c.png?raw=true" alt="usb-c connection" width="30%" height="auto"></div>|
| |<div align="center"><img src="https://github.com/respawnin/screendget38-docs/blob/main/imgs/screendget-macropad.png?raw=true" alt="macropad" width="70%" height="auto"></div> | <div align="center"><img src="https://github.com/respawnin/screendget38-docs/blob/main/imgs/screendget-media-controller.png?raw=true" alt="media controller" width="70%" height="auto"></div>|
| | Assign macropad as master using `setmaster`  | Assign media controller as node using `setnode`|


All devices will automatically communicate via the chain after their roles are set.

----------

## **RGB Lighting**

Each Screendget macropad and the media controller includes an **internal RGB LED** positioned in the central light chamber.  
This LED provides quick at-a-glance status, layer indication, or theming to match your setup.

### **Changing LED Colour**

Use the `rgb` command to set the LED colour.

#### **Syntax**

    rgb R G B

Where **R**, **G**, and **B** range from **0–255**.

#### **Examples**

Set the LED to purple:

    rgb 128 0 255

Turn off the LED:

    rgb 0 0 0