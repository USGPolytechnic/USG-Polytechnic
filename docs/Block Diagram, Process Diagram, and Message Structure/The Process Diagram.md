[Process Diagram](https://app.diagrams.net/#G1YnGLDMCkIUuk0xOXI2Jxs83gCzxwHKuU#%7B%22pageId%22%3A%22pc2VwhXcHSOIUS0fXVyV%22%7D)

![Screenshot 2025-03-08 002553](https://github.com/user-attachments/assets/378fe910-acfc-4388-b1a4-41c9dcc8e059)

---
# Communication Sequence Functionality & Requirements Alignment

Our sequence diagram captures the end-to-end flow of data and control between the Web User, ESP32 Wi-Fi/Cloud subsystem, HMI, Sensor board, and Motor board. Below we dissect each major functional step, illustrating how it meets both user needs and the product requirements.

---

## 1. User-Initiated Data Request  
**Flow:**  
1. **Web User → MQTT Server**  
   - User clicks “Get Weather Data” in the companion app or browser.  
2. **MQTT Server → ESP32 (Web Subsystem)**  
   - ESP32 subscribes to a “request/data” topic and immediately receives the trigger.  

**Function & Benefits:**  
- **On-Demand Control:** Empowers remote users to manually refresh data, satisfying the requirement for interactive, user-driven queries.  
- **Decoupled Architecture:** By using MQTT topics, the Web-to-device link is robust to network fluctuations and scales to multiple clients without modifying embedded code.

---

## 2. Sensor Polling & Response  
**Flow:**  
1. **ESP32 → PIC18F (Sensor Subsystem)** via UART  
   - Frames a **Request Sensor Data** message (Type 0x0002) with Source=T, Dest=E.  
2. **PIC18F → ESP32** via UART  
   - Replies with **Sensor Data Response** (Type 0x0003), packing temperature (×100), humidity (×100), and flow rate (×100) in a single 64-byte frame.

**Function & Benefits:**  
- **Deterministic Timing:** UART exchange completes in under 50 ms, ensuring end-to-end latency stays well below the 500 ms target.  
- **Compact, Scalable Data:** Packing three sensor readings in one frame reduces bus traffic and simplifies parsing on both ends.  
- **Error Detection Ready:** Fixed headers/footers allow both boards to detect framing errors and respond with an Error Message if needed.

---

## 3. Local Display Update & Actuator Control  
**Flow:**  
1. **ESP32 → PIC18F (HMI Subsystem)** via UART  
   - Sends an **LCD Update Command** (Type 0x0004) including a formatted text string:  
     ```
     “Temp: 25.5°C, Hum: 50.1%, Flow: 10.5 L/min”
     ```  
2. **ESP32 → PIC18F (Motor Subsystem)** via UART (if temperature threshold exceeded)  
   - Sends a **Set Water Flow** command (Type 0x0001) with desired flow rate.  
3. **PIC18F (Motor) → ESP32 & HMI**  
   - Acknowledges with a **Sensor Data Response** echoing new actuator state, and publishes a **Motor Status** update to the HMI display via another LCD Update Command.

**Function & Benefits:**  
- **Immediate Local Feedback:** Users at the exhibit see current values and actuator state on the I²C LCD within tens of milliseconds.  
- **Automatic Control Logic:** Temperature-driven “if > threshold, send flow command” logic runs on the ESP32, providing hands-free regulation—key for agricultural demos.  
- **Consistent UX:** All subsystems use the same framing and ID scheme, reducing firmware complexity and improving maintainability.

---

## 4. Cloud Publication & Remote Monitoring  
**Flow:**  
1. **ESP32 → MQTT Server**  
   - Publishes a **Cloud Update** message (Type 0x0005) serialized as JSON, containing `{ "temp":2550, "hum":5010, "flow":1050 }`.  
2. **MQTT Server → Web User**  
   - Distributes the updated payload to all subscribed dashboards in real time.

**Function & Benefits:**  
- **Real-Time Remote Visibility:** Stakeholders off-site can monitor conditions live, fulfilling the “online rapid updates” requirement.  
- **Standardized Data Format:** JSON payloads enable easy integration with third-party analytics or mobile apps without additional parsing code on the microcontrollers.

---

## 5. Error Handling & Safety  
**Flow:**  
1. **Any MCU → ESP32 (or upstream board)**  
   - On detect­ed framing, sensor, or communication failure, sends an **Error Message** (Type 0x0006) with subsystem ID and ASCII error string.  
2. **ESP32 → HMI & Web**  
   - Displays the error on the LCD and publishes an alert topic via MQTT.  
3. **Fail-Safe Actuation**  
   - Motor board, upon detect­ing “sensor offline” or repeated framing errors, automatically shuts down the actuator.

**Function & Benefits:**  
- **Robust Diagnostics:** Clear error propagation ensures fast troubleshooting during demos or field use.  
- **User Safety:** Automated motor shutdown on critical faults prevents uncontrolled water flow—meeting safety requirements for all-age exhibits.

---

### Summary of Functional Alignment  
- **Latency & Predictability**: Deterministic framing and prioritized message types guarantee sub-second loops.  
- **Bi-Directional Control**: Both manual (web) and automatic (threshold-based) command paths exist.  
- **Scalability & Maintainability**: Uniform message format and modular blocks simplify adding new sensors or actuators.  
- **Educational Transparency**: Each step—from request through actuation—is explicit, making it easy for students to trace and understand in the exhibit setting.  
- **Reliability & Safety**: Error messages and fail-safe logic are integral to the sequence, ensuring the system remains stable and secure under fault conditions.

---
Top 5 changes to software desingn
---
### Top 5 Biggest Changes to Software Design Since the Software Proposal  

1. **Sensor Rework and Integration**  
   Initially, the team encountered issues with sensor selection, requiring multiple iterations to find a reliable temperature and humidity sensor. The previous sensors either failed due to voltage inconsistencies or were incompatible with the system’s communication protocol. The team ultimately selected the **AHT21**, which offered stable data transmission and was easy to integrate using **I2C communication**. This change ensured accurate environmental readings, improving system functionality and satisfying project requirements. The **UML sequence diagram** illustrates how sensor data is properly transmitted via **WiFi and UART**, ensuring reliable communication with the MQTT system and motor subsystem.  

2. **HMI Rework for User Interaction and Proper Display**  
   The initial HMI design lacked clarity in displaying temperature and humidity readings, creating difficulties for user interaction. The team reworked the HMI structure to properly visualize real-time environmental data, ensuring that users could access updates efficiently. The improvements included optimizing **SPI communication** and refining **display logic**, ensuring that sensor readings were correctly formatted. This refinement is reflected in the **sequence diagram**, where the **HMI now processes and displays information** received from the MQTT system and motor drive, ensuring proper user feedback.  

3. **Byte System Redesign for Data Transmission**  
   The initial approach to **byte-based communication** caused misinterpretations between subsystems, leading to incorrect actuator responses and inconsistent data flow. The team redefined the **8-byte structure**, ensuring each subsystem clearly understands its role and can process messages accurately. This involved assigning **specific bytes** to **source ID, destination ID, message data, and control flags**, ensuring seamless integration between the **sensor, motor drive, MQTT system, and HMI display**. The **UML diagram** highlights structured message transmission, demonstrating how systems now exchange properly formatted data without errors.  

4. **MPLAB Code Functionality and API Integration**  
   Initially, there were significant challenges in implementing **MPLAB code** for the **PIC microcontroller**, particularly in defining the API structure for subsystem communication. The team overcame this issue by carefully debugging the MPLAB code and structuring the API so that identification of users and devices followed a logical format. This update allowed **proper recognition of commands** from different components, ensuring seamless message routing. The **UML sequence diagram** now correctly represents this improved interaction, showing how messages flow from the sensor subsystem to the motor drive and MQTT system without data loss or misinterpretation.  

5. **Synchronization of Sensor Data Across Subsystems**  
   One of the biggest challenges was ensuring that sensor data was **properly translated** across all subsystems so that every component remained in sync. Early versions of the system had **timing mismatches**, causing incorrect actuator responses. The team resolved this by refining **data transmission timing**, adding **delays** where necessary, and ensuring that **each subsystem processes temperature readings in real time**. The **UML diagram** illustrates how information is processed correctly through structured communication delays, ensuring smooth synchronization across all components.  

These refinements ensure that the system meets **user needs, project specifications, and class requirements**, improving both **functionality and real-world applicability**. The **UML sequence diagram** validates these changes by accurately depicting **sensor communication, actuator responses, data transmission, and user interaction** throughout the system.

