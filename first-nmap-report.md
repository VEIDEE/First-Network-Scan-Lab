# First Nmap Scan

## Summary
I performed an Nmap scan on a Windows virtual machine (10.0.2.3) to identify open ports and services.

## Findings
- The host is up and reachable
- 995 ports are filtered/protected
- Port 5357 is open (Web Services API)

## Analysis
The scan shows that most ports are protected, reducing the attack surface. However, port 5357 is open and could be investigated further.

## Conclusion
The system has limited exposed services, but the open port represents a potential entry point that should be monitored or secured.



## Service Detection

A more detailed scan was performed using the `-sV` flag to identify the service and version running on the open port.

### Results
- Port 5357 is running Microsoft HTTPAPI httpd 2.0
- The service uses HTTP and is associated with SSDP/UPnP

### Analysis
This indicates that the target system is running a Windows-based web service. While this is a legitimate service, exposed HTTP services can sometimes be targeted for vulnerabilities.

### Conclusion
The additional scan provides deeper insight into the exposed service, which is useful for both attackers and defenders when assessing potential risks.



## Advanced Scan

An advanced scan was conducted using the `-A` flag to gather additional information about the target system.

### Results
- The system is running a Microsoft Windows operating system
- OS detection suggests Windows 10 or Windows 11 (92% confidence)
- Port 5357 is running Microsoft HTTPAPI 2.0
- The HTTP service returned "Service Unavailable"

### Analysis
The scan confirms that the target is a Windows-based system with an exposed HTTP service. Although the service is not actively serving content, it still represents a potential attack surface.

### Conclusion
The advanced scan provides a deeper understanding of the system, including OS identification and service behavior, which are essential for both offensive and defensive analysis.



## Full Port Scan

A full port scan was done using the `-p-` flag to identify all open ports on the target system.

### Results
- Port 5040 is open (unknown service)
- Port 5357 is open (Web Services API)
- Port 7680 is open (Windows Update Delivery Optimization)

### Analysis
The full scan revealed additional open ports that were not detected during the first scan. This shows the importance of using in depth scans when assessing a system.

Port 5040 is particularly interesting as the service is currently unknown, which may require further investigation.

### Conclusion
The system has multiple exposed services, increasing the potential attack surface. Further analysis would be required to determine whether these services pose a security risk.



## Service Interaction

A manual connection was attempted to port 5040 using netcat.

### Result
- A connection was successfully established
- No immediate response or banner was received from the service
- No response was received, even after sending input

### Analysis
The lack of response suggests that the service may require specific input or communication protocol. This makes it more difficult to identify and may require further investigation.

### Conclusion
Port 5040 is active and accepts connections, but does not provide output, making it an interesting target for deeper analysis.



## HTTP Service Interaction

An HTTP request was sent to port 5357 using curl.

### Result
- The service responded with HTTP Error 503 (Service Unavailable)
- The response included HTML content

### Analysis
This confirms that the service is an active HTTP-based service. Although it is not currently serving usable content, it is still accessible and responding to requests.

### Conclusion
HTTP service that responds but is unavailable may indicate a misconfiguration or restricted service. Further testing could determine if additional endpoints or functionality exist.



## Script-Based Analysis

An Nmap scan using default scripts (`-sC`) was ran against port 5357.

### Result
- The service was identified as WSDAPI
- No additional information or vulnerabilities were found

### Analysis
The default scripts did not reveal any further details about the service. This suggests that the service does not expose easily identifiable weaknesses or misconfigurations.

### Conclusion
The service appears to be operating normally without showing additional information through standard automated checks -sC.