# Network-Anomaly-Detection-Cybersecurity-EDA-Project

## What is this project about?

Every network has thousands of sessions happening every second. Most are normal but some are attacks. The goal of this project is to find those suspicious sessions using data analysis and machine learning without any predefined rules.


## Dataset

Source: Kaggle — Cybersecurity Intrusion Detection Dataset
9,537 sessions with 55% normal and 45% attack traffic
Features include login attempts, session duration, browser type, encryption, IP reputation and failed logins


## What I found — EDA Insights

Failed logins turned out to be the strongest signal. Normal sessions averaged 1.18 failed logins while attack sessions averaged 1.94 — almost double. This single feature alone separates a large chunk of attack traffic.

Session duration told an interesting story. Normal users finish sessions within 0 to 2000 seconds. Attackers stayed much longer with some sessions going beyond 4000 to 7000 seconds. This is consistent with data exfiltration behavior where an attacker needs time to copy data out.

Packet size was completely useless. Despite intuition network packet size showed almost no difference between normal and attack traffic — 501 vs 498. Not every feature that sounds important actually is.

Unknown browser type was the most suspicious category with a 73% attack rate compared to around 43% for Chrome Firefox and Edge. This likely indicates automated bots or unsophisticated attackers who don't bother spoofing their browser identity.

Sophisticated attackers actually used higher reputation IPs — not lower. This was a surprising finding. It suggests that advanced attackers use trusted infrastructure to bypass perimeter defenses rather than obviously malicious IPs. Classic APT behavior.

Encryption type had minimal impact overall. AES showed the lowest attack rate at 43.6% followed by DES at 45.3% and Unknown at 46.2% — suggesting either unencrypted sessions or deliberate obfuscation techniques.


## Anomaly Detection

Instead of rule based detection I used Isolation Forest — an unsupervised ML algorithm that isolates unusual sessions based on all features combined rather than a single threshold.

477 suspicious sessions were flagged out of 9537 total. Anomaly sessions showed session durations of 1557 seconds on average compared to 752 seconds for normal sessions — more than double. Login attempts were also consistently higher in flagged sessions.


## Detection Priority Based on This Analysis

If building a simple detection system from scratch based on these findings the priority order would be to first check failed logins as the strongest signal then login attempts then session duration then flag unknown browser types and finally avoid relying on IP reputation alone since it was consistently misleading for sophisticated attackers.


## What this taught me

Traditional security systems often block based on IP reputation or packet size. Both turned out to be weak signals in this dataset. Behavioral signals like session duration and failed logins are far more reliable. This is exactly why modern security platforms use AI based behavioral analysis instead of static rules — because sophisticated attackers have already learned to bypass the static ones.


## Tools Used

Python, Pandas, Matplotlib, Seaborn, Scikit-learn, Google Colab

## Dataset

Kaggle — Cybersecurity Intrusion Detection Dataset
kaggle.com/datasets/dnkumars/cybersecurity-intrusion-detection-dataset
