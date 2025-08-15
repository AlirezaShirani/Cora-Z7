# Cora Z7-10 Ethernet (ENET0) Setup in Vivado

This guide describes how to configure the **Cora Z7-10** board in Vivado for Ethernet communication using the Zynq-7000 Processing System (PS) **ENET0** interface.

---

## Steps

### 1. Create a New Vivado Project
1. Open Vivado.
2. Select **New Project**.
3. Set your **Project Name** and **Location**.
4. Under **Project Type**, select **RTL Project** (do not specify sources at this stage).
5. Under **Default Part**, choose **Boards** tab → **Cora Z7-10**.

---

### 2. Create Block Design
1. Go to **Tools → Create Block Design**.
2. Name your design (e.g., `cora_z7_eth`).
3. Click **OK**.

---

### 3. Add Zynq Processing System
1. In the Block Design, click **Add IP**.
2. Search for **ZYNQ7 Processing System** and add it.
3. Click **Run Block Automation** and confirm default settings.

---

### 4. Configure ZYNQ7 for Ethernet
Double-click the **ZYNQ7 Processing System** block to open the configuration menu.

#### 4.1 PS-PL Configuration
- Navigate to **PS-PL Configuration → General**.
- **Enable Clock Resets** → **Deactivate**.
- Go to **AXI Non-Secure Enablement → GP Master AXI Interface**.
  - **M AXI GP0 Interface** → **Deactivate**.

#### 4.2 Enable Ethernet 0
- Go to **Peripheral I/O Pins**.
- Find **Ethernet 0** → Set to **Active**.

#### 4.3 Assign MIO Pins for ENET0
- Go to **MIO Configuration → I/O Peripherals**.
- Set **ENET0 MIO 16..27** → **Active**.

#### 4.4 Enable MDIO
- In **MIO Configuration → I/O Peripherals**, set:
  - **ENET0 → MDIO MIO 16..27** → **Active**.

#### 4.5 Clock Configuration
- Go to **Clock Configuration → PL Fabric Clocks**.
- Set **FCLK_CLK0** → **Deactivate**.

---

## Next Steps
Once ENET0 is enabled and MIO pins are assigned, export the hardware to **Vitis** and create a networking application (e.g., using **lwIP**).

---

## Notes
- This configuration uses the Processing System's Ethernet directly; no PL logic is required.
- Ensure your Cora Z7-10 board files are installed in Vivado for automatic MIO pin mapping.
