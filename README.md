**Level-Control_PLC_TIA-Portal_S7-1215C_KTP400**

Developed entirely in TIA Portal v15.1 using Structured Text (SCL), with no third-party libraries.
The function block is fully optimized for the S7-1215C AC/DC/Rly, keeping a lean and maintainable structure with room for future expansion.
It's about a basic level control system for pump management.
This project integrates a Siemens S7-1215C PLC with a KTP400 Basic HMI to provide real-time level monitoring, variable-speed pump control, and a clear status indicator workflow.      

<<<< CAUTION: NO EMERGENCY CONTROL LOGIC IS IMPLEMENTED >>>>  

🚀 System Overview  
This project implements a closed-loop liquid level control process,, featuring:  
* Analog Level Monitoring (manual level entry via HMI): Reads a Level Indicating Transmitter (LIT) signal (0–27648 analog range) with built-in safety clamping to guard against out-of-range values.  
* Proportional Pump Power: Motor power is calculated inversely proportional to tank level — the lower the level, the higher the pump output — ensuring smooth, continuous control.  
* Three-State Status Logic: Discrete indicators (H1/H2/H3) reflect LOW, OK, and HIGH level states, both on physical outputs and mirrored to the HMI.  
* Safety Envelopes: Input and output values are both clamped in software, ensuring the motor never receives a negative power setpoint and the analog signal stays within valid bounds. 
* HMI Integration: All key process variables (motor power, status indicators) are mirrored to HMI tags for live operator visibility.     

🛠 Hardware Stack  
* PLC: Siemens S7-1215C AC/DC/Rly    
* HMI: Siemens KTP400 Basic    
* Development Environment: TIA Portal v15.1    
* Language: Structured Control Language (SCL / Structured Text) 
* Level Sensor: Any analog Level Indicating Transmitter (LIT) 0-10V      
* Any Frequency Inverter (depends on motor pump power)    
* Any AC motor pump (depends on process load)        


📂 Project Structure  
/Level_Control.zip        — Full TIA Portal v15.1 PLC project (ready to open and download)  
/PUMP_CONTROL.scl         — Standalone copy of the SCL source code for quick review  
/System_Overview          — Sketch of hardware connections and wiring  
/Screenshots              — HMI screenshots and TIA Portal configuration views    


⚙ Operational Flow    
* Normal Operation (10% < Level < 90%): H3 indicator active; pump runs at proportional power relative to current level.  
* Low Level (≤ 10%): H1 indicator active; pump runs at near-maximum power to refill the tank quickly.  
* High Level (≥ 90%): H2 indicator active; pump is released (disabled) to prevent overflow.  
* Motor Power Calculation: POWER_SP = (1 - LIT / 27648) × 100% — fully linear, no PID is used in this application.  
* Safety Clamping: LIT is clamped to [0, 27648] and POWER_SP is floored at 0 before being applied to the motor  
* NO EMERGENCY CONTROL IS IMPLEMENTED       


📜 License  
This project is licensed under the Creative Commons Attribution-ShareAlike 4.0 International (CC BY-SA 4.0).  

☕ If this project is helpfull for your application, please consider to support:  
https://www.paypal.com/donate/?hosted_button_id=8S8BJ9TT368VN

Built by rafamuratt: https://murat-tech.eu/  
Murat-Tech Channel: https://www.youtube.com/@Murat-TechChannel-EN 
