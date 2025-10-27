### **Reflection**  

#### **Lessons Learned**  
Throughout the development of this project, the team gained valuable insights into **system design, communication protocols, and problem-solving techniques**. Below are the top ten lessons learned:  

1. **Thorough Hardware Testing is Essential** – Many unexpected issues arose due to sensor failures, improper voltage regulation, and soldering errors. Careful testing and debugging helped resolve these issues.  
2. **Strict Adherence to Datasheets Prevents Issues** – Following hardware reference designs correctly, particularly for **microcontrollers and voltage regulators**, avoids hours of unnecessary troubleshooting.  
3. **Message Structure Must Be Clear and Consistent** – Initial versions of our **byte-based message format** led to misinterpretation among subsystems. Reworking this structure improved communication clarity.  
4. **Software Debugging Requires a Methodical Approach** – Debugging MPLAB code required structured testing using **logical debugging tools** rather than trial-and-error approaches.  
5. **Synchronization Between Subsystems is Critical** – Each component operates at different speeds, requiring proper **timing delays** to prevent miscommunication between the sensor, actuator, and user interface.  
6. **Modular Code Design Improves Scalability** – Dividing software into smaller, manageable sections allowed us to troubleshoot individual modules without affecting the entire system.  
7. **Real-Time Monitoring Enhances System Reliability** – Using an **MQTT server** ensured constant data availability, allowing users to remotely view **temperature and motor states**.  
8. **Wireless Communication Adds Complexity** – WiFi and Bluetooth integration introduced additional points of failure, highlighting the importance of structured error handling.  
9. **Cross-Team Collaboration is Key to Success** – Clear communication between team members ensured that everyone’s **subsystem aligned properly** with the overall system objectives.  
10. **Project Constraints Require Adaptability** – Flexibility in adjusting **sensor selection, actuator control, and communication protocols** allowed us to overcome roadblocks effectively.  

#### **Recommendations for Future Students**  
1. **Understand Communication Protocols Early** – Learning about **UART, I2C, SPI, and MQTT** beforehand will streamline development.  
2. **Follow the Datasheets Precisely** – Always double-check **voltage ratings, timing requirements, and pin configurations** before designing circuits.  
3. **Use Debugging Tools Efficiently** – Utilize tools like **Logic Analyzers, Serial Monitors, and MPLAB Simulations** to identify and correct software errors.  
4. **Manage Time Wisely** – Software debugging, hardware assembly, and testing **always take longer than expected**—allocate extra time for troubleshooting.  
5. **Work Closely with Your Team** – Keeping all members informed on **design decisions and code implementations** ensures a smooth development process.  

#### **Version 2.0: Improving Communication Architecture**  
If we were to develop a **Version 2.0** of the communication architecture, several improvements could enhance **system reliability, debugging, and expandability**:  

- **Refined Byte Structure**: Instead of using a rigid **8-byte message format**, a more **dynamic, expandable protocol** would allow easier modification for future updates, accommodating additional sensor types or actuator functions.  
- **Enhanced Debugging Capabilities**: Implementing **error-detection bytes** and logging mechanisms directly into the message structure would make **troubleshooting communication failures** significantly easier.  
- **Optimized Code Division**: Separating **sensor reading logic, motor control functions, and display operations** into distinct software modules would improve maintainability and scalability.  
- **Improved Wireless Communication Reliability**: Adding **redundancy checks** for WiFi and Bluetooth signals ensures **smooth data transmission** without unexpected loss.  
- **Integration of More Peripherals**: Expanding functionality by including **additional sensors, more advanced motor control features, and improved data visualization methods** would enhance overall usability.  
- **Simplified Protocol Design**: Adopting a **standardized packet format**, similar to MQTT or Modbus, would allow for **easier expansion**, making it **more robust for real-world applications**.  

These refinements would not only enhance system performance but also **simplify debugging and improve long-term reliability**, ensuring that the architecture remains **adaptable and scalable** for future applications.
