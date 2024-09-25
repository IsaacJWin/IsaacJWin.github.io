# Diagram of a small scale DDoS Attack
```mermaid
sequenceDiagram
participant Attacker
Create Participant BotNet
Attacker->>BotNet: 1. Infects many computers<br/>to control
box black Attackers
participant Attacker
participant BotNet
end
Attacker->>BotNet: 2. Orders all infected computers<br/>to send requests to Webserver
Participant LegitimateTraffic
Participant Firewall
participant WebServer
box blue Website
participant Firewall
participant WebServer
end
BotNet->>WebServer: 3. All computers send requests multiple times
WebServer->>BotNet: 4. Responds to all requests, slowing or stopping traffic
LegitimateTraffic-xWebServer: 5. Unable to connect or slow connection
Firewall->>BotNet: 6. Notices high traffic from same IPs, limits rate of requests
BotNet-xFirewall: 7. Attempts to send more requests, gets rate limited
Firewall->>WebServer: 8. Notifies server of<br/>high traffic
WebServer->>Firewall: 9. Tells Firewall to<br/>add high traffic IPs<br/>to blacklist
BotNet-xFirewall: 10. Blacklisted, unable to reach server
LegitimateTraffic->>WebServer: 11. Able to connect
```
## Steps explained
1. A BotNet is a collection of computers infected by malware that is controlled by a central attacker
2. Botnets typically include many computers of the same kind, as the malware controlling and infecting them must work on all infected systems
3. A large amount of requests can slow a server down if the server cannot handle the amount of traffic
4. A server may be unable to tell apart malicious traffic and normal traffic at first
5. The primary goal of a DDoS attack is to disable normal functions of a victim, which for a website means stopping normal traffic
6. A firewall can limit the amount of traffic from all IPs, which may help if the firewall isn't also overwhelmed
7. The rate limit can come in the form of requiring a captcha image to be completed, or simply disallowing connection to the serve for a short time
8. Many security programs have ways to notify owners of issues, including unusual ammounts of traffic
9. If an IP is blacklisted, it will not be allowed through the firewall. This may also catch legitimate traffic attempting to reach a server during a DDoS attack, or simply during a period of high traffic, so be careful when blacklisting
10. While blacklisting is a solution, if the firewall is overwhelmed checking the IPs, it can stop normal traffic from getting through. Many attackers also have the ability to "Spoof," or fake, the IP address shown to a firewall, and can get through this way as well
11. While the shown solutions can work, they may only work on the smaller scale, and larger amounts of requests can only be handled by more powerful and more numerous hardware. More sophisticated attacks specifically target the firewall, and those have different methods of defense