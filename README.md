# Malicious Access Point Detective (MalAP Detective)

**Note: The `main` branch only contains this `README.md`. Please find the corresponding source code under other branches.**

This is a tool used for detecting malicious access point. From our perspective, we assume that the malicious AP do DNS spoofing attack and ARP spoofing attack. As for DNS spoofing attack, we proposed a polymerized method using public DNS verification APIs by our distributed servers on TLS, to reach the standard of CIA(Confidentiality, Integrity and Accessibility). This is a proxy-like method.

## System Overview
![NUSSWS drawio](https://github.com/vivalayan/MalAP_Detection/assets/90449797/ecf06e92-012a-47dd-9380-85df1939bfd2)
## Prize
![SWS3011_Second Prize](https://github.com/vivalayan/MalAP_Detection/assets/90449797/a6a52592-a806-4773-baa9-c7e91846c9b3)



## 1.Team members
- @vivalayan
- @melody0123
- @ChaoHanley
- @SuiseiKawaii
- @YuanHansen2233

## 2.Deployment

Our DNS spoofing detector adopts the server-client model. In order to make it work on your own machine, please follow the instructions here. As the server is polymerized, we only need to deploy server.py since it contains both root server and branch server implementations.

### 2.1 Deploy the Root Server

1. Go to the `Server` branch. Clone the whole branch from the repository.
2. Follow the instructions in README.txt to set up the runtime environment.
3. Launch the server with the command `python3 Server.py`

### 2.2 Deploy the Branch Server

The root server and branch server are integrated into one program so the deployment steps are the same.

1. Go to the `Server` branch. Clone the whole branch from the repository.
2. Follow the instructions in README.txt to set up the runtime environment.
3. Launch the server with the command `python3 Server.py`

### 2.3 Deploy the Client

1. Download and install JDK-19.

2. Go to the `dns-spoofing-client` branch. Clone the whole branch from the repository.

3. Create a `config.properties` file at the root directory of the client. The content should be look like this.

   ```
   ROOT_IP=123.123.123.123
   ROOT_PORT=4433
   ```

   Please fill in the `ROOT_IP` field with the IPv4 address of your root server. Please do **NOT** modify the `ROOT_PORT` field unless you want the server to run on another port.

4. Import CA Certificate into the Truststore

   Since we used self-signed certificate, so on the client machine, you will need to import the self-signed CA certificate into the Java truststore, which stores the trusted certificates for  SSL/TLS connections. We use the default truststore here. The default truststore for Java is usually located  at `<JRE_HOME>/lib/security/cacerts`. You can use the `keytool` command to import the CA certificate:

   ```
   keytool -import -trustcacerts -alias myCA -file ca_certificate.crt -keystore cacerts
   ```

   Replace `myCA` with the desired alias name, `ca_certificate.crt` with the filename of the CA certificate, and `cacerts` with the path to the Java truststore (you may need administrator privileges to modify this file).

   **Note: We have already provided you with a self-signed CA certificate, which is `testCA.crt`, located in the root directory of the client. Therefore, the `ca_certificate.crt` should be the `testCA.crt`.** 

5. Modify the Java Program

   Go to `/src/Client.java`. Find line 80 to 83 and change them according to your own configuration made in step 4.

6. Open and run the project with IntelliJ IDEA.

## 3 Overview

This is a tool for end users to detect malicious access point on their own machines.

## 4 Functions

### DNS spoofing detection
Sniffing DNS queries on host machine, then send those queries to our VeriDNS server. After verification, host can see the results on console.
### ARP spoofing detection 
[Click here](https://github.com/Melodys-Code-Warehouse/MalAP-Detective/tree/arp-spoofing)
