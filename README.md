# Subdomain Enumeration

## Project goal
You must map a target domain for subdomains using amass and Sublist3r, then show how to reduce the attack surface. You must document findings and recommend mitigation steps.

Context and rules I set
I worked on a lab domain you approved.
I used a snapshot before testing.
I limited scans to avoid service disruption.
I recorded timestamps and outputs for reproducibility.

## Phase 1, prep
I installed amass and updated wordlists.
Commands I ran:
sudo apt update, sudo apt install amass

<img width="1147" height="811" alt="image" src="https://github.com/user-attachments/assets/c435df67-67a5-4c4b-beff-e0d3e73f161a" />

## Phase 2, passive enumeration
I ran passive lookups to gather known records without touching the target DNS resolvers directly. That reduces noise and legal risk.

## Command:
amass enum -passive -d example.com -o hi_subs_passive.txt/amass enum -passive -d example.com -o passive.txt

<img width="865" height="129" alt="image" src="https://github.com/user-attachments/assets/d3ee1300-4a83-4a3e-8fa0-5caaaf9f5368" />

What you get, example
Passive lookup returned 197 candidate names and 5 distinct IP ranges in the example run.

## Phase 3, active enumeration
When you have permission, run active probes to discover hidden hosts. Start small and increase scope.

## Command:
amass enum -active -d example.com -o active.txt

<img width="686" height="214" alt="image" src="https://github.com/user-attachments/assets/435f8cb9-d41e-4086-a31e-2a5d2d6dc735" />


Tips
Start with port-limited checks, for example test only 80 and 443 to avoid overloading services. Use -timeout and -rate options to throttle queries.






















Subdomain Enumeration using Sublist3r






