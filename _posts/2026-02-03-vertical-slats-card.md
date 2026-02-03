---
layout: post
title: "Building a Vertical Blinds Card I Actually Trust"
date: 2026-02-03
author: Your Name
categories: [Home Assistant, Lovelace, UI Design]
tags: [home-assistant, hacs, lovelace, blinds, ui]
excerpt: "Vertical blinds look simple until you try to represent them honestly in Home Assistant. This is the story of how I stopped fighting the hardware and built a card around its limits."
---

I didn’t set out to build a custom Lovelace card.

I just wanted my vertical blinds to *make sense* in Home Assistant.

In the room itself, it’s obvious what’s happening. The slats rotate. Light comes in or it doesn’t. You can tell at a glance whether the blind is open or closed.

In Home Assistant, though, most vertical blind motors only expose two actions: **open** and **close**. No tilt position. No percentage. No feedback. Just a binary switch pretending to represent something much more nuanced.

That mismatch bothered me more than I expected.

---

## The problem with pretending everything is a slider

The obvious solution is to fake it.

Add a slider. Animate the slats. Guess how long the motor takes to move. Call it “tilt” and move on.

I’ve done that before. It looks good for a while. And then, inevitably, it drifts out of sync. The UI says one thing, the room says another, and trust quietly evaporates.

Once that happens, you stop believing the dashboard.

I didn’t want another card like that.

---

## Letting go of precision

The moment things clicked was when I stopped trying to *measure* the slats and started treating them as **purely visual**.

Instead of asking “what angle are the slats at?”, I asked a simpler question:

> What does the user expect to *see* after they press open or close?

That’s where the Vertical Slats Card came from.

There’s no real tilt control. No percentages pretending to mean something. Just a visual representation that reflects the **last thing you told the blinds to do**.

An `input_number` helper stores that visual state. It doesn’t claim to be feedback. It doesn’t pretend to be smart. It just remembers intent.

That separation felt surprisingly honest.

---

## What it actually looks like

Here’s the same blind, shown closed and open.  
Nothing fancy is happening behind the scenes. The animation is driven entirely by the helper value.

<div style="display:flex; gap:2rem; justify-content:center; flex-wrap:wrap; margin:2rem 0;">

  <div style="text-align:center;">
    <img src="/img/card-closed.png"
         alt="Vertical Slats Card – closed"
         style="width:50%; max-width:400px; border-radius:12px;">
    <p style="opacity:0.7; font-size:0.9em;">Closed</p>
  </div>

  <div style="text-align:center;">
    <img src="/img/card-open.png"
         alt="Vertical Slats Card – open"
         style="width:50%; max-width:400px; border-radius:12px;">
    <p style="opacity:0.7; font-size:0.9em;">Open</p>
  </div>

</div>

It doesn’t claim to know what the hardware can’t tell it. And because of that, it rarely feels “wrong”.

---

## Why I cared about fabric

Most vertical blind cards I’ve seen look like plastic.

Mine aren’t.

Fabric blinds absorb light. They don’t sparkle. Highlights are soft, wide, and uneven. If you exaggerate that effect, it looks fake. If you get it right, you stop noticing it entirely.

That was the goal.

Muted colors. Subtle gradients. Just enough variation between slats to suggest weight and material, without drawing attention to itself.

If you notice the effect immediately, I’ve probably overdone it.

---

## Light-aware visuals, but only visually

One feature I went back and forth on was reacting to daylight.

In the end, I allowed **lux-based auto-tinting**, but with a hard rule:  
it could only affect appearance.

If you have an outdoor light sensor, the slats can look slightly lighter in bright daylight and slightly deeper in low light. That’s it.

No movement. No automation logic. No decisions being made for you.

The card stays a display, not a controller.

---

## The things I deliberately didn’t add

There are a lot of things people expect a blinds card to do that this one doesn’t:

- no tilt slider  
- no partial angles  
- no timing-based guesses  
- no per-slat control  
- no automation hooks  

Those aren’t missing features. They’re lines I didn’t want to cross.

Every one of those would have made the UI *feel* smarter while actually being less truthful.

---

## Learning to stop

One of the hardest parts of this project wasn’t writing the code. It was deciding when to stop adding things.

The card does one job: it shows vertical blinds in a way that feels consistent with how the hardware actually behaves.

That narrow focus is probably why it ended up being accepted into HACS with very little friction.

And now that it’s there, I’m intentionally leaving it alone for a while.

If feature requests come in that strengthen this idea, great. If not, that’s fine too. Stability is underrated.

---

## Links

- GitHub repository:  
  https://github.com/nfmsh/vertical-slats-card

- Available via HACS → Frontend

---

If there’s one thing this project reinforced for me, it’s this:

**A UI doesn’t need to be clever to be good.  
It just needs to be honest.**