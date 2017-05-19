# Introduction to Threat Modeling
Speakers: Ying Li, David Lawrence

(I missed the first few minutes, and walked in in the middle of an analogy about security protocols in houses/cars: front doors, etc.)

+ Enumerate the expected entry points to each entity in your app.
+ Also list all the unintentional entry points to each entity in your app (e.g. a robber could come in thru a window if the window is configured incorrectly)
+ List the 'valuables' in your system: user generated content, credit card numbers, etc.
+ Enumerate all the trust-level/privilages, and their hierarchies: resident/admin, guest/moderator, visitor/registered user, passerby/anonymous user.
+ Diagram all your data flows
  + single process (single cirle),
  + multi-process (double circle),
  + external dependency (box),
  + data store ( double line),
  + data flow (solid arrow),
  + trust boundary (dotted line)
    + It's **really important** to analyze what info crosses each trust boundary.

"Hard shell, soft center" <-- NOT a good security model.  Once actor is in, just trust them.  Assume they authenticated correctly.

## STRIDE  <-- categories of vulnerability in your system.
+ S: spoofing
  + brute force
  + csrf
  + "Let me in, I'm a plumber" <-- how can you tell?  Maybe it's a robber who's casing your place.
+ T: tampering
  + violating the integrity of data in some way
  + e.g. an indoor smoker covering the smoke detector so they can get away w/ smoking inside
  + SQL injection
+ R: repudiation
  + Keeping track of who did which (malicious) actions
  + rm -rj /var/log
+ I: information disclosure
  + bad messaging
  + SQL injection
  + MITM
+ D: Denial of service
  + SQL Injection, DDOS
  + 'gluing shut the locks to your house'
+ E: elevation of privilage
  + SQL injection
  + CSRF

## Prioritization of vulnerability
1. Impact: what's the worst that can happen if someone takes advantage of this weakness?
2. Probability: how likely is it that someone can find & exploit the weakness?

Use the answers to these questions to score your existing vulnerabilities.  How you weight impact vs. probability depends on your specific needs.

Another scoring system:

### DREAD
+ D: damage potential
+ R: reproducibility
+ E: exploitability
+ A: affected users
+ D: discoverability

Impact = damage potential + affected users

Probabiltiy = reproducibility + exploitability + discoverability

## Remediate

+ spoofing: solve w/ authentication
  + user auth
  + request auth
+ tampering: solve with integrity controls
  + validate input
  + checksums
+ repudiation: solve w/ "non-repudiation" (i.e. audit trails)
  + append-only logs
  + digital signatures
+ information disclosure: solved w/ confidentiality
  + encryption (at rest and in transit)
  + redaction
  + configuration
+ denial of service: solve w/ availability
  + more replicas
  + rate limiting
  + recovery protocols
+ elevation of privilage: solve w/ authorization
  + defined auth model
  + least privilage
  + re-authorization

## System integration

How to do all of the above across an entire system of apps?

+ Make sure to add any new components to the threat model.
+ Keep your deploy/infrastructure config up-to-date w/ the structure of your app
+ Keep your own threat models up to date.  Abide by the security requirements of any 3rd party packages that your apps use, and make sure you're up to date on those.

## In summary
1. Collect data about your app
2. Analyze the data (STRIDE)
3. Remediate
   + Prioritize (impact scoring/DREAD)
4. Iterate

## Resources:
+ OWASP




