
Postmortem: The Great Proxy Pass Fiasco
Issue Summary: The Day NGINX Went Rogue
Duration of the Outage:

Start Time: August 3, 2024, 17:00 EAT
End Time: August 3, 2024, 18:30 EAT
Impact:
Our beloved e-learning platform decided to take an unscheduled coffee break, leaving users staring at 502 Bad Gateway errors—like showing up to a study session only to find the classroom door locked. For 90 minutes, 100% of our users were unable to access the site, leading to confusion, frustration, and a noticeable drop in productivity.

Root Cause:
The root cause of the outage was a misconfiguration in the NGINX server. Specifically, a typo in the proxy_pass directive caused NGINX to route requests to an invalid upstream server, leading to the 502 errors experienced by all users.

Timeline: A Comedy of Errors
17:00 EAT: 🍕 Tea Time?—An automated alert notified us that the site was returning 502 errors. It seems NGINX decided to go on break.
17:05 EAT: The on-call engineer, halfway through his cup of chai, confirmed the outage. The 502 error was no joke.
17:10 EAT: The engineer assumed the Flask back-end had taken a nap and restarted it, hoping to get things back on track. But no, Flask was wide awake and waiting for work.
17:20 EAT: Realizing it wasn’t the back-end’s fault, the engineer escalated the issue to the DevOps team. Time to get serious.
17:40 EAT: DevOps discovered the culprit: a misconfigured proxy_pass directive in the NGINX configuration. It was like asking for directions and getting pointed to a dead end.
17:50 EAT: After correcting the configuration, NGINX was reloaded. The web server was back in action, and the site started to come back online.
18:00 EAT: The site was tested, and users could once again access the platform. Crisis averted.
18:30 EAT: The incident was officially resolved, and normal operations were fully restored.
Root Cause and Resolution: The Real Villain Was... a Typo
Root Cause:
A small but critical typo in the NGINX configuration file caused the proxy_pass directive to misroute requests, leading to the 502 Bad Gateway errors. This error effectively cut off communication between NGINX and the Flask back-end, leaving users stranded.

Resolution:
The issue was resolved by identifying and correcting the typo in the NGINX configuration file. The corrected configuration was reloaded, restoring proper routing and resolving the 502 errors.

Corrective and Preventative Measures: Lessons Learned (and Some Free Therapy)
Improvements:

NGINX, Meet CI/CD: We’ll add automated configuration checks to our CI/CD pipeline to prevent this from happening again. NGINX is now under close watch.
Monitoring 2.0: Our monitoring will be enhanced to include specific alerts for proxy errors. No more rogue typos slipping through the cracks.
Tasks:

Patch the NGINX Config: Double-check all proxy_pass directives. They’re sneaky little devils.
Add Config Validation: Automate NGINX configuration validation before it hits production.
Upgrade Monitoring: Enhance error detection for NGINX, focusing on proxy errors.
Team Training: DevOps bootcamp, anyone? Let's refresh our best practices.
Document the Madness: Update the playbook with new lessons, and add a section on "Avoiding the Tyranny of Typos."
Final Thoughts:
If there’s one thing we’ve learned, it’s that even the smallest mistake can cause major headaches. Here’s to smoother deployments and typo-free configurations!

And remember, always proofread your NGINX configs. It’s the difference between a smooth operation and a 90-minute panic attack. 🎉
