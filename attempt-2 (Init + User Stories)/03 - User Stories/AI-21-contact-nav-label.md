# AI-21: Contact Navigation Label

## Title
Change "Connect with an Expert" to "Contact" as primary navigation label

## User Story
As an **older adult or non-native English speaker**, I want **the primary navigation to use the standard "Contact" label**, so that **I can quickly find how to get in touch without confusion**.

## Acceptance Criteria

- [ ] Primary navigation shows "Contact" (not "Connect with an Expert")
- [ ] "Contact" is used consistently across all pages and CTAs in the main nav
- [ ] "Connect with an Expert" may remain as secondary text on the Contact page itself
- [ ] Link is clearly identifiable and accessible

## How to Test

1. View the site and locate the primary navigation.
2. Verify the link label is "Contact" (not "Connect with an Expert").
3. Check all pages for consistency; verify main nav uses "Contact" everywhere.
4. Verify the Contact page can still use "Connect with an Expert" as descriptive/subheading text.
5. Have an older adult or non-native speaker confirm they can identify the Contact link immediately.

## Developer Notes

- Change nav link text from "Connect with an Expert" to "Contact."
- Can keep "Connect with an Expert" as secondary text on the Contact page itself.
- Ensure consistent use of "Contact" across all pages and CTAs in the main navigation.
- Update any aria-labels or link text that reference the old label.
- Verify no broken links or references after the change.

## WCAG References

- **2.4.4 Link Purpose (In Context) (Level A):** The purpose of each link can be determined from the link text alone or from the link text together with its programmatically determined link context.
- **3.2.4 Consistent Identification (Level AA):** Components that have the same functionality within a set of Web pages are identified consistently.

## Priority
**P3 Medium**

## Effort Estimate
**Small (30 min)**
