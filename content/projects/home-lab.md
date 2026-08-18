---
title: Privacy-First AI Home Lab
shortTitle: Home Lab
description: My self-hosted setup for local AI, home automation, and a voice assistant I can take apart and improve.
date: 2024-01-01
lastmod: 2026-08-17
weight: 1
status: Active
role: Designer, operator, and test engineer
featured: true
tech:
  - Proxmox
  - Linux
  - Home Assistant
  - Zigbee
  - Ollama
  - Hermes
  - Raspberry Pi
  - Pi-hole
highlights:
  - label: Runs on
    value: Virtualized, self-hosted services
  - label: AI
    value: Local inference with Ollama
  - label: Device control
    value: Home Assistant automations
  - label: Current work
    value: Qualifying the first voice satellite
---

This started with Home Assistant and a Zigbee network about a year ago. I wanted better home automation and an excuse to learn the parts of the stack I had never owned myself. It kept growing. The lab now runs several isolated services under Proxmox, including Home Assistant, Pi-hole, local models through Ollama, and a Hermes assistant.

The interesting part is getting those pieces to work together without handing one AI agent the keys to everything. Hermes handles the conversation. Ollama serves the local model. Home Assistant stays in charge of device actions. I can change or replace one piece without rebuilding the whole setup.

## The voice satellite

The newest piece is a Raspberry Pi voice satellite. It hears a wake word, captures speech, passes the request through Home Assistant, and plays the response through a speaker. It can also carry out a small reversible automation that I use as the end-to-end test.

Getting that first full exchange working felt like a real milestone. Then I rebooted it and checked that it came back on its own. I am still working through audio consistency, offline behavior, and rebuildability before I call it finished.

## Local AI on ordinary hardware

I use local inference whenever it is good enough for the job. It keeps more of the interaction on equipment I control and gives me room to experiment without metering every request. It also makes hardware limits impossible to ignore. Model choice, context length, and response time all become practical engineering decisions.

Hermes replaced an earlier assistant setup. I kept the old environment available until the new one worked and its recovery path was tested. Moving the useful knowledge was straightforward; keeping credentials out of anything portable took more care.

## The bugs are the useful part

One of my favorite problems started with the assistant giving the wrong time. The AI was fine. The voice pipeline was fine. The real cause was a time-sync issue created by an unexpected interaction between services. I traced it through the system, fixed the service behavior, and ran the voice test again.

That episode is a good example of why I keep working on the lab. Installing a service is usually the easy part. Understanding what happens when several services disagree is where the project gets interesting.

## How I work on it

I make one bounded change at a time and keep a way back. New integrations start small, usually with observation or a harmless test action. Once the behavior is repeatable, I decide whether it deserves more responsibility.

My QA background shows up everywhere. I test restarts and failed paths, not only the demo that works. I write down what “done” means before widening the scope. That discipline lets me experiment without turning the lab into something I am afraid to touch.

## On the bench now

Right now I am finishing the first voice satellite and making its recovery process reproducible. After that I want to explore infrastructure monitoring, isolated development workflows, more voice nodes, and room-aware interactions. A custom wake word and local voice are on the list too, mostly because they sound fun to build.
