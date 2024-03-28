#Especially-Safe

This project demonstrates a secure Wi-Fi node for ESP32 microcontrollers from Espressif Systems, prioritizing encrypted communication with three potential layers:

1. **WPA2/WPA3 Wi-Fi Network Encryption** (recommended for most deployments)
2. **TLS/SSL Encryption** for secure data transfer using algorithms like AES-GCM or ChaCha20Poly1305 (depending on server and client capabilities)
3. **Client Certificate Authentication** (optional, not implemented in this code but possible for a 3rd layer)

**Features:**

* Connects to a Wi-Fi network using secure WPA2/WPA3 encryption.
* Establishes a secure connection to a server using:
    - `WiFiClientSecure` for encrypted communication.
    - Trusted Root Certificate Authority (CA) to verify server identity (1st layer of encryption).
* Performs an HTTP GET request to a server (optional security check using [https://www.howsmyssl.com/](https://www.howsmyssl.com/)).
* Flashes LEDs for visual indication (optional).

**Hardware Requirements:**

* ESP32 microcontroller (consult your specific ESP32 board's documentation)
* LEDs (red, green, blue)
* Resistors (values depend on LED specifications)
* Breadboard and connecting wires

**Software Requirements:**

* Arduino IDE ([https://www.arduino.cc/en/software](https://www.arduino.cc/en/software))
* ArduinoJson library ([https://arduinojson.org/](https://arduinojson.org/)) (if needed for parsing server responses)
* WiFiClientSecure library (included in Arduino IDE)

**Configuration:**

**1. Wi-Fi Credentials:**

- Replace `<WIFI_SSID>` and `<WIFI_PW>` in the code with your Wi-Fi network name and password.

**2. Cloudflare DNS (Optional):**

- Improve performance and potentially enhance security by using Cloudflare's DNS servers:

```c++
const char* dnsServerIP = "1.1.1.1";
WiFi.config(dnsServerIP);  // Set DNS server after WiFi connection
```

**3. Server and Root CA:**

- The code currently uses `howsmyssl.com` for verification. You can replace the server address (`server`) and root CA certificate (`test_root_ca`) if needed.

**Encryption Algorithms:**

- **Wi-Fi Encryption (assumed):** WPA2/WPA3, likely using AES-CCM or similar algorithms.
- **TLS/SSL Encryption:** Typically uses TLS 1.2 or higher, employing AES-GCM or ChaCha20Poly1305 for data encryption and message authentication (specific algorithms depend on server and client capabilities).

**Understanding the Code:**

1. **Includes and Definitions:**
   - Necessary libraries (`WiFiClientSecure.h`, `Wire.h`, etc.)
   - Constants for screen size (if using an OLED display), LED pins, Wi-Fi credentials, server address, and the root CA certificate.

2. **OLED Display Setup (Optional):**
   - Initializes the OLED display (if connected) for visual feedback.

3. **Cloudflare DNS (Optional):**
   - Configures Cloudflare's DNS server after connecting to the Wi-Fi network.

4. **LED Pin Setup:**
   - Configures the LED pins as outputs.

5. **Wi-Fi Connection:**
   - Attempts to connect to the specified Wi-Fi network using the provided credentials.
   - Displays connection status messages on the serial monitor.

6. **Secure Client and Server Connection:**
   - Creates a `WiFiClientSecure` object for secure communication.
   - Loads the root CA certificate to verify the server's identity.
   - Attempts to connect to the server using HTTPS (port 443).

7. **HTTP GET Request (Optional):**
   - If connected, sends an HTTP GET request to the server and reads the response (potentially using the ArduinoJson library for parsing JSON responses).

8. **LED Blinking (Optional):**
   - Alternates flashing red, green, and blue LEDs for visual indication (can be customized).

**HowsMySSL.com Verification:**

This code can be used with [https://www.howsmyssl.com/](https://www.howsmyssl.com/) for a basic security check of the server you're connecting to.

Also I have tested this project and verified it through wiresharks logs to test the encryption.

![LOG](https://github.com/HimuCodes/Especially-Safe/assets/110077858/708c1661-dcbb-4764-b5e2-2c3467a41fe5)

![Screenshot 2024-01-21 104931](https://github.com/HimuCodes/Especially-Safe/assets/110077858/3e49acb7-f481-496c-8e96-1c37048142e4)

Poster for the project:![Especially Safe!](https://github.com/HimuCodes/Especially-Safe/assets/110077858/bdad213b-f4af-4683-8de4-6e72c186e3cd)



