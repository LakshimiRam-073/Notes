# Lecture-to-Notes Skill — Suggested Optimizations

Based on generating notes for 6 lectures (Memory Hierarchy, VM Concepts, VM Details, Malloc Basic, Malloc Advanced), here are improvements that would make the skill better.

---

## 1. Add a "Clarity-First" Writing Principle

**Problem:** The current skill says "be comprehensive" but doesn't emphasize clarity. Some generated sections transcribe the professor's explanation nearly verbatim rather than *teaching* the concept.

**Fix:** Add to the Writing Guidelines section:
```
For each concept, follow this order:
1. WHY — What problem does this solve? (1-2 sentences)
2. PLAIN ENGLISH — Explain it like the student missed class (no jargon yet)
3. HOW — The mechanism, with diagrams and code
4. EXAMPLE — Concrete worked example with real numbers
5. CONNECT — How does this relate to the previous section?
```
This prevents the "wall of transcript" problem where notes read like a transcript dump rather than structured teaching.

---

## 2. Add ASCII vs Mermaid Decision Matrix to SKILL.md

**Problem:** The current Visual Descriptions section was updated with guidelines, but agents still over-use Mermaid for simple things or under-use it for complex flows.

**Fix:** Add a concrete decision table:

| Concept Type | Use | Example |
|---|---|---|
| Bit field layout | ASCII | `[VPN (8 bits) | VPO (6 bits)]` |
| Memory block layout | ASCII | Heap blocks with headers/footers |
| Simple grid/table | ASCII | DRAM supercell array, page table entries |
| Linear memory map | ASCII | Process address space |
| Hardware internals | ASCII | Disk platters, chip pinouts |
| Access pattern | ASCII | Stride-1 arrows through array |
| Multi-step flow with decisions | Mermaid flowchart | Cache hit/miss, page fault handling |
| Multi-actor interactions | Mermaid sequence | Memory read/write transactions |
| System architecture with subgroups | Mermaid flowchart | CPU-MMU-TLB-Cache-Memory |
| Multi-level hierarchy | Mermaid flowchart | Memory hierarchy pyramid |

---

## 3. Line Count Target Should Be a Range, Not a Floor

**Problem:** The skill says "minimum 750 lines" which causes agents to pad notes or over-explain trivial concepts just to hit the number. Some sections end up verbose for no reason.

**Fix:** Change to: "Target 750–1000 lines. Under 750 means you likely missed content. Over 1100 usually means you're padding. If the lecture is genuinely short or simple, 600 well-written lines beats 800 padded lines."

---

## 4. Add "Buggy Code" Handling Guideline

**Problem:** Lectures like Malloc Advanced have many intentional bugs in code examples. The current skill doesn't have guidance on how to present buggy code vs correct code.

**Fix:** Add to the Code Examples section:
```
When the professor shows buggy code:
1. Show the buggy code first in a code block
2. Add a ⚠️ callout: "Can you spot the bug?"
3. Explain what's wrong in plain English
4. Show the fixed version
5. Explain WHY the fix works

Format:
⚠️ **Bug:** [one-line description]
**Wrong:** `*size--` (decrements the pointer, not the value)
**Right:** `(*size)--` (decrements the pointed-to value)
```

---

## 5. Add "Section Transition" Sentences

**Problem:** Notes sometimes jump from one topic to the next without explaining *why* we're switching. The reader loses the narrative thread.

**Fix:** Add guideline: "Between major sections, include a 1-2 sentence transition that connects the previous topic to the next. E.g., 'Now that we understand WHY dynamic allocation exists, let's look at HOW the allocator actually manages memory.'"

---

## 6. Enforce Consistent Glossary Format

**Problem:** Glossary entries vary in quality. Some are one-word definitions, others are multi-sentence.

**Fix:** Standardize: "Each glossary term should have: the term in bold, a concise definition (1-2 sentences), and optionally a slide reference. Example:
- **Page Table Entry (PTE)**: A record in the page table that maps a virtual page number to a physical page number (or marks the page as not present). 📊 Slide 14"

---

## 7. Add Cross-Lecture References

**Problem:** Lecture 14 (Malloc Advanced) builds on Lecture 13 (Malloc Basic), and Lecture 12 (VM Details) builds on Lecture 11 (VM Concepts). But the notes don't link to each other.

**Fix:** Add guideline: "If this lecture is part of a series, include a 'Prerequisites' line at the top:
```
> 📋 **Prerequisites:** [Lecture 11: VM Concepts](./11-vm-concepts-notes.md)
```
And cross-reference specific sections when relevant: 'See [Lecture 13, Section 7: Implicit Free Lists](./13-malloc-basic-notes.md#7) for the coalescing algorithm.'"

---

## 8. Add Exam Tip Callouts

**Problem:** Professors often say things like "this will definitely be on the exam" or "students always get this wrong." The current skill captures these as regular quotes, but they deserve special formatting.

**Fix:** Add: "When the professor hints at exam relevance, use a special callout:
```
📝 **Exam Tip:** The professor emphasizes that students confuse internal vs external fragmentation. Internal = wasted space INSIDE an allocated block. External = enough total free space exists but it's not contiguous.
```"

---

## Summary of Priority

| Optimization | Impact | Effort |
|---|---|---|
| Clarity-first writing order | 🟢 High | Low — just add to guidelines |
| ASCII vs Mermaid decision matrix | 🟢 High | Low — already partially done |
| Line count range not floor | 🟡 Medium | Low |
| Buggy code handling | 🟢 High | Low |
| Section transitions | 🟡 Medium | Low |
| Glossary format | 🟡 Medium | Low |
| Cross-lecture references | 🟡 Medium | Low |
| Exam tip callouts | 🟡 Medium | Low |

All are low-effort additions to the SKILL.md that would noticeably improve output quality.
