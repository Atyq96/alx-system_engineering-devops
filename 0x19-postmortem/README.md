Postmortem: The Great Load Balancer Fiasco of May 25, 2024

When you realize your load balancer just lost its balance

Issue Summary
Duration of Outage:
Start: May 25, 2024, 10:15 AM GMT
End: May 25, 2024, 12:30 PM GMT
Total Duration: 2 hours 15 minutes

Impact:
Our beloved web application took a nap, affecting 75% of our users. They were greeted with the charming "503 Service Unavailable" error. The remaining 25% got to play the refreshing game of "Will it Load?" with slow responses and intermittent connectivity.

Root Cause:
Our load balancer decided to play favorites, sending too much traffic to a few servers and leaving the rest idle. This overload made the servers cry and crash. Turns out, an incorrect setting during the last update made it act like an overzealous bouncer at a club, letting everyone into one door.

Timeline
10:15 AM GMT: Our monitoring system shouted, "Something's wrong!" High error rates and server downtime detected.
10:20 AM GMT: On-call engineer starts playing detective with the alert.
10:30 AM GMT: First guess: "Must be the database acting up."
10:40 AM GMT: Database checks out fine. The plot thickens. Focus shifts to application servers.
11:00 AM GMT: Servers are overloaded like a buffet at lunchtime. Suspect a memory leak. Restart attempt #1.
11:15 AM GMT: Restart fails. Servers still cranky. Call in the network team – they bring donuts.
11:30 AM GMT: Network team spots uneven traffic. The load balancer's configuration looks guilty.
11:45 AM GMT: Bingo! Load balancer misconfiguration found.
12:00 PM GMT: Reconfigure the load balancer to share the love (traffic).
12:30 PM GMT: Traffic normalized. Servers happy. Users happy. We are happy. Outage resolved.
Root Cause and Resolution
Root Cause:
The load balancer was set to a static traffic distribution mode instead of dynamic, making it overwork a few servers while others were on a break. This setting was accidentally changed during a routine update, causing the traffic jam.

Resolution:
We reverted the load balancer to its previous dynamic mode, ensuring a fair distribution of traffic. After tweaking the configuration file and testing it under various traffic conditions, we restarted the servers to clear any residual hiccups.

Corrective and Preventative Measures
Improvements and Fixes:

Configuration Management: No more cowboy changes. Strict change management for load balancer settings.
Monitoring Enhancements: Smarter monitoring to catch load balancer tantrums sooner.
Redundancy: Backup load balancers to avoid putting all eggs in one basket.
Documentation and Training: More how-to guides and training for our tech wizards.
Task List:

 Patch the load balancer to the latest version with all the bells and whistles.
 Set up alerts for any load balancer configuration tweaks.
 Review and optimize current load balancer settings.
 Regular incident response drills focused on load balancer issues.
 Update internal knowledge base with new findings and steps.
 Implement a regular restart schedule for application servers to avoid overloads.
By addressing these areas, we aim to keep our system running smoothly and avoid any more surprise naps. Stay tuned for more adventures in web stack management!
