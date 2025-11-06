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





## Subdomain Enumeration using Sublist3r

# Project goal
Map a client domain for subdomains with Sublist3r, then show how to reduce risk. You document findings and give clear fixes.

Story, step by step
1. Prep the lab
 Clone the repo and install requirements.

 Command: git clone https://github.com/aboul3la/Sublist3r.git


<img width="664" height="304" alt="image" src="https://github.com/user-attachments/assets/2bc5ac50-b7c9-4851-ad8e-7bd71afd9dfa" />

2. Quick passive sweep
Run passive first to avoid extra DNS traffic.

## Command:

sublist3r -d yoursite.com -o passive.txt

Passive results give known candidates from public sources.

Example result: passive.txt lists 12 candidates

<img width="1110" height="826" alt="image" src="https://github.com/user-attachments/assets/1312b09f-10fd-442c-8b24-4fc9e2b43101" />

# Active enumeration, controlled pace

Increase scope slowly. Test a few ports only.

sublist3r -d yoursite.com -o active.txt

<img width="957" height="690" alt="image" src="https://github.com/user-attachments/assets/0b455977-9826-4f07-b719-43098062888f" />


## Remediation steps, prioritized

1. Prevent DNS zone transfers
2. Close exposed panels-move admin interfaces behind VPN or IP allow list, not public internet.
3. Prevent CNAME takeovers-remove records pointing to third party services you no longer use.
4. Enforce access control- enable MFA on DNS and cloud accounts, rotate keys monthly.
5. Add monitoring and automation-run this scan weekly and alert on new resolves or new CT entries.

## Practical commands you can paste

1. Quick passive run:

sublist3r -d yoursite.com -o passive.txt

2. Active run:

sublist3r -d yoursite.com -o active.txt

3. Brute run with wordlist:

sublist3r -d yoursite.com -b -w /path/to/wordlist.txt -o brute.txt






