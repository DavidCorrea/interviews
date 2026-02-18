# Story 04: Make Link Labels Unique and Descriptive

## User Story

**As a** screen reader or voice control user,
**I want** every link on the page to have a unique, descriptive label,
**So that** I can identify and activate the correct link without relying on visual context.

## Description

There are 6-7 "Learn More" links on the homepage that are all identically labeled. Screen reader users cannot distinguish them in a links list. Voice control users saying "Click Learn More" are presented with a numbered overlay of 7 options with no way to tell which is which. The LinkedIn "Connect" link is also ambiguous alongside the "Connect with an Expert" CTA.

## Acceptance Criteria

- [ ] No two links on the same page share identical visible text unless they point to the same URL
- [ ] Each "Learn More" link includes context: e.g., "Learn More about AI Automation" (visible text or `aria-label`)
- [ ] The LinkedIn link reads "Connect with LaunchPad Lab on LinkedIn" (not just "Connect")
- [ ] A screen reader links list shows distinct, meaningful labels for every link
- [ ] Voice control users can uniquely target any link by speaking its label

## Testing Instructions

1. **Screen reader:** Open the homepage with NVDA or VoiceOver, pull up the links list (NVDA: Insert+F7; VoiceOver: VO+U) — verify every link has a unique, descriptive label
2. **Voice control:** Using Dragon NaturallySpeaking or Voice Control (macOS), say "Click Learn More" — there should be no ambiguous overlay of identically-named links
3. **Manual audit:** Tab through all links on the homepage and note the announced text for each — no duplicates
4. **Subpages:** Repeat the audit on the contact page, service pages, and case study pages

## Metadata

| Field | Value |
|-------|-------|
| **Priority** | Critical |
| **Complexity** | Low |
| **WCAG Criteria** | 2.4.4 (Link Purpose in Context), 2.4.9 (Link Purpose Link Only) |
| **Affected Users** | Screen reader users, voice control users, ADHD users |

## Source Reports

- Screen Reader Report
- Voice Control Report
- ADHD User Report
