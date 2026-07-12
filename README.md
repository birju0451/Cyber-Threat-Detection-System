This is the most important design decision of your project. If you only use a Random Forest model trained on phishing URLs, your project will only detect known attack patterns. Your teacher will definitely ask:

"How will your system detect a new attack that is not present in the training dataset?"

So instead of building only a signature-based detection system, we'll build a Hybrid AI Cyber Threat Detection System.

Final Detection Architecture
                    Cyber Threat Detection System
                               │
        ┌──────────────────────┼──────────────────────┐
        │                      │                      │
 Signature Detection     Anomaly Detection      Rule-based Detection
        │                      │                      │
 Random Forest          Isolation Forest       Security Rules
 XGBoost                One-Class SVM          Blacklist
                        Autoencoder*           Whitelist
                               │
                     Threat Confidence Score
                               │
                          Final Decision
Detection Type 1: Signature-Based Detection (Known Attacks)
Purpose

Detect attacks that are already present in the training data.

Detects
Phishing URLs
Fake login pages
Malicious domains
Suspicious URL structures
Model
Random Forest (Primary)
XGBoost (Comparison)
Example

Known phishing URL:

http://paypal-login-security.xyz

Random Forest

Prediction:

Phishing
98% confidence
Detection Type 2: Anomaly Detection (Unseen Attacks) ⭐⭐⭐

This is the innovation that makes your project stronger.

Instead of asking:

Is this URL phishing?

The model asks:

Does this URL look abnormal compared to legitimate URLs?

Even if the attack is completely new...

https://secure-login-paytm-verification-new.ai

...the anomaly detector can still flag it as suspicious because its features differ from normal URLs.

Algorithms
Isolation Forest ⭐⭐⭐⭐⭐ (Recommended)

Best for:

Unknown phishing URLs
Zero-day URLs
Novel attacks

Advantages

No labels required
Fast
Excellent for anomaly detection
One-Class SVM

Learns only legitimate URLs.

Anything very different becomes suspicious.

Useful for:

Unknown domains
Rare attack patterns
Autoencoder (Optional - Advanced)

Uses Deep Learning.

Learns:

Normal Behaviour

If reconstruction error is high:

Unknown Threat

This is a good extension if you have time.

Detection Type 3: Rule-Based Detection

Machine learning is powerful, but some threats can be identified instantly with simple rules.

Examples:

URL length > 120

↓

Suspicious
Contains IP Address

↓

Suspicious
Too many subdomains

↓

Suspicious
Many special characters

↓

Suspicious
Executable downloaded

↓

Alert
Known phishing domain

↓

Block immediately
Detection Type 4: Reputation-Based Detection

Compare domains with trusted and malicious lists.

Safe
google.com
github.com
microsoft.com

↓

Trusted

Malicious
Known phishing list

↓

Blocked

Data Sources

PhishTank
OpenPhish
URLHaus
Detection Type 5: Behaviour Detection

Instead of looking only at URLs...

Watch what happens on the system.

Examples

Browser suddenly opens

↓

Unknown URL

↓

Downloaded EXE

↓

Process Started

↓

Internet Connection Created

↓

Alert

Monitor

Downloads

Running processes

Browser URLs (where feasible)

File creation

Executable launches

Detection Type 6: Download Detection

When a file is downloaded:

example.exe

Check

Extension

↓

Hash

↓

Size

↓

File name

↓

Risk Score

↓

Alert

Detection Type 7: Process Detection

Monitor running processes.

Examples

powershell.exe
cmd.exe
wscript.exe
unknown.exe

Check

Parent process

CPU usage

Network usage

Execution path

Detection Type 8: Threat Scoring (Innovation)

Instead of simply saying:

Safe

or

Phishing

Give a score.

Example

Detection Module	Score
Random Forest	90
Isolation Forest	80
Rule Engine	95
Reputation	100
Behavior	70

Final Score

Threat Score = 87%

Decision

0–30

Safe

31–60

Suspicious

61–100

Malicious

This makes your project look much more like a commercial security product.

Final Detection Flow
User opens URL
        │
        ▼
Feature Extraction
        │
        ▼
Random Forest
        │
        ▼
Isolation Forest
        │
        ▼
Rule Engine
        │
        ▼
Reputation Check
        │
        ▼
Threat Score Calculation
        │
        ▼
Desktop Notification
        │
        ▼
Store in Database
Why This Can Detect Unseen Attacks

Traditional ML models classify only what they've seen during training. To improve on that:

Random Forest/XGBoost handles known phishing patterns.
Isolation Forest flags unusual URLs and behaviors, even if they weren't in the training set.
Rule Engine catches obvious indicators (IP-based URLs, excessive subdomains, suspicious file extensions, etc.).
Behavior Monitoring watches for suspicious actions after a download or process starts.
Threat Scoring combines all these signals into a final decision instead of relying on a single model.

Important: No system can guarantee detection of every unseen (zero-day) attack. Your hybrid approach improves the chances of detecting previously unseen threats by combining anomaly detection, rule-based analysis, and behavioral monitoring with supervised ML. This is a technically sound claim and is appropriate to present in a final-year project.

Final Models for Your Project
Module	Model/Technique	Purpose
Known URL Detection	Random Forest	Detect known phishing URLs
Unknown Attack Detection	Isolation Forest	Detect unseen/anomalous URLs
Rule Engine	Custom Python Rules	Instant heuristic detection
Reputation Engine	Blacklist/Whitelist	Detect known malicious domains
Background Monitor	watchdog + psutil	Monitor downloads and processes
Threat Fusion	Risk Score Engine	Combine all evidence into one decision