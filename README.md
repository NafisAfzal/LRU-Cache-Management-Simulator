# Simulating Cache Management Policies to Reduce Pollution and Thrashing in C Using LRU

A CSE 360 academic report on simulating a small CPU cache to demonstrate cache pollution, thrashing,
and Least Recently Used (LRU) replacement behavior. This repository publishes the final approved
report; it does not include a separate runnable source-code project.

## Project Overview

The report models a CPU cache with four entries and a simple access trace. Frequently used data
(the "working set") is mixed with one-off accesses (the "pollution"). Each access updates a logical
timestamp, and the least recently used entry is evicted when the cache is full. The simulation shows
how LRU keeps the working set in the cache and reports hits, misses, and the final cache contents.

## Objectives

- Model a small cache and observe how unnecessary data can displace useful data.
- Demonstrate cache pollution and the resulting thrashing behavior.
- Apply LRU replacement to protect frequently reused entries.
- Show hit/miss activity and final cache state through serial output.

## Background

**Cache pollution** occurs when one-off accesses fill the cache and push out frequently used data.
When the processor repeatedly has to fetch that data from slower main memory, performance degrades —
a condition described in the report as **thrashing**. LRU addresses this by tracking when each entry
was last used and discarding the oldest entry first.

## Implementation Overview

The report contains the complete C-style sketch. Its main elements are:

- A `CacheLine` structure with `tag`, `valid`, and a timestamp field.
- `CACHE_SIZE` set to 4 and `MEMORY_SIZE` set to 50.
- A global logical clock (`globalClock`) that advances on every request.
- An access pattern of `{1, 2, 99, 1, 2, 98, 1, 2, 97, 1, 2}`.
- Functions for cache access, insertion, LRU eviction, and state printing.
- Serial output at 115200 baud for real-time hit/miss observation.

The included output screenshots report 11 requests, 6 hits, 5 misses, and a final cache containing
`{1, 2, 97, 98}`, with the message `SUCCESS: Cache Pollution avoided.`

## Cache Management Policy

**LRU (Least Recently Used):** on a hit, the entry's timestamp is refreshed; on a miss, the entry is
inserted if space is available. When the cache is full, the entry with the smallest timestamp is
replaced. This protects the working set (`1` and `2`) from being displaced by single-use accesses
(`99`, `98`, `97`).

## Technologies Used

- C / Arduino-style sketch with `setup()` and `loop()`
- Serial Monitor output (`Serial.begin(115200)`)
- ESP32 Dev Module reference in the output screenshot
- CPU cache concepts: working set, pollution, thrashing, LRU replacement

## Team Members

The original academic work was completed collaboratively by:

- Nafis Afzal
- Fahim Monaym
- Jalal Uddin Mohammad Rumi
- Istiaque ahmed
- Md Ahsiul Karim

## Course Information

- **Institution:** East West University, Department of Computer Science and Engineering
- **Course:** CSE 360 — Computer Architecture
- **Semester:** Fall 2025
- **Section:** 05
- **Submitted to:** Md. Adnan Morshed, Lecturer
- **Submission date:** 17/12/2025

## Final Report

[Download the final approved report (PDF)](Simulating_Cache_Management_Policies.pdf)

The report is 7 pages and contains the project description, features, full code listing, and output
screenshots. It is the only report version published here.

## Academic Attribution

All academic content, implementation, and findings are credited to the CSE 360 team listed above.
Repository preparation, documentation organization, and publication maintenance were performed by
Nafis Afzal; these activities do not change the original collaborative authorship of the report.

No open-source license has been granted. The repository is public for academic and reference
purposes only; public visibility does not grant permission to reuse, copy, or redistribute the
report.
