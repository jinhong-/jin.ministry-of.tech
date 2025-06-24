---
layout: post
title:  "Help, Someone's Hogging the EV Charging Lot"
date:   2025-06-25 00:30:00 +0800
categories: []
---

I don’t own an EV yet — though I’d love to someday. But like many others, I’ve seen and read stories about EV charging lots being misused. In high-density estates or malls where charger availability is limited, it's especially frustrating when EV drivers can’t charge simply because someone else is hogging the lot.

Many EV charging providers have started implementing **overstay fees** to discourage idle charging, but there are two common situations that still slip through the cracks:

1. **An EV is parked but not plugged in**  
2. **A non-EV vehicle is parked in the lot**

These scenarios block access to legitimate users and waste valuable infrastructure.

## The Design Constraints

I started brainstorming solutions with two key goals:

1. **Low deployment cost**  
2. **Vendor-agnostic compatibility** — something that could work with any EV charger and carpark system.

Here’s what I landed on — a simple, scalable approach that can be applied across many public and private carparks.

## My Solution: Flap-Based Deterrence

We use **parking flap barriers** as the enforcement mechanism. Why flap barriers?

- They're **much cheaper** than in-ground bollards  
- They require **minimal civil works**  
- They're **easy to retrofit** in most carparks  

Rather than preventing entry, the system **raises the flap only if the lot is misused**. Think of it as a quiet enforcer — always down unless someone breaks the rules.

## How It Works

- We display **clear signage** at each EV lot: misuse will incur a fee.
- If misuse occurs, the user is required to **scan a QR code and pay the fee online** before the flap will lower.
- The flap system integrates with the EV charger via the **OCPP protocol**, so we can detect when a valid charging session begins.
- If no session is detected within a **15-minute grace period**, we raise the flap to block the car from leaving until the penalty is paid.

### The typical flow:
1. An EV enters the charging lot.
2. The user has **15 minutes** to plug in and begin charging.
3. If they do — great, nothing happens.
4. If not — the flap raises, and the user must **pay a usage fee** via QR to exit.

We also apply the same logic **after a session ends** — the driver has 15 minutes to leave the lot. This gives users fair buffer time while ensuring turnover.

## Why This Works

This system:
- **Discourages non-charging EVs and unauthorised cars** without requiring heavy infrastructure
- **Works with any OCPP-compliant charger**
- **Deters misuse without delaying compliant users**
- **Shifts enforcement to the hardware**, not carpark staff or app warnings

The beauty is in its simplicity — we’re not reinventing the charger. We're just making sure people use it responsibly.

PS: I don't claim to be an expert in any of these. This is just a simple thought experiment on how this challenge can be solved. The ideas are my own, though i cannot claim that this does not already exist, and isn't already patented/protected somehow. And of course I used ChatGPT to brainstorm and to also help me write this
