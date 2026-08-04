# Open Source

**Date:** 2026-08-04
**Category:** Technology & Systems

## What It Is

Open source refers to software (or designs, hardware specs, documentation) whose **source code is made publicly available**, along with a license that grants people the right to **view, use, modify, and redistribute** it. It's defined by a license, not just by being visible - code posted publicly with no license, or "all rights reserved," is not open source.

## The Core Distinction: Free as in Freedom vs. Free as in Price

- **Free (libre)** - you have the *freedom* to inspect, change, and share the code.
- **Free (gratis)** - the software costs $0.

Open source guarantees the first. It does **not** technically require the second - a license can even permit commercial resale, as long as the freedoms are preserved. In practice, almost all open source software is also free of cost, but the two concepts are legally and philosophically separate.

## Official Criteria (Open Source Definition, maintained by the Open Source Initiative)

1. **Free redistribution** - no charging royalties or fees to redistribute the software
2. **Source code included** - must be distributed with, or made easily available alongside, the compiled program
3. **Derived works allowed** - modifications and derivative software must be permitted, under the same license
4. **Integrity of the author's source code** - some licenses may require modifications be distributed as patches, preserving the original
5. **No discrimination against persons or groups**
6. **No discrimination against fields of endeavor** - e.g. can't say "not for use in business" or "not for use in genetics research"
7. **License applies automatically** to anyone who receives the software, no separate agreement needed
8. **License must not be specific to a product** - rights don't disappear if the code is extracted into a different project
9. **License must not restrict other software** distributed alongside it
10. **License must be technology-neutral** - can't require a specific interface or technology

## License Types (the split that matters most in practice)

| Type | Behavior | Examples | Use case |
|------|----------|----------|----------|
| **Permissive** | Very few restrictions - can be used in closed-source/commercial products | MIT, Apache 2.0, BSD | Businesses building proprietary products on top |
| **Copyleft** | Anything built on top must also stay open source under the same license | GPL, AGPL | Projects that want derivatives to stay open forever |

Companies routinely avoid GPL-licensed dependencies in proprietary products because of this "share-alike" requirement - this distinction shows up constantly in real engineering decisions.

## Related but Different Concepts

- **Public domain** - no owner, no license, no restrictions at all (different from open source, which still has an author and a license)
- **Freeware** - free to use, but source code is usually *not* available (not open source)
- **Source-available** - code is visible but the license restricts modification/redistribution (not open source under the OSD)

## Real-World Examples

- **Linux kernel** - GPL-licensed, copyleft
- **Python** - permissive license
- **pytest / Selenium ecosystem** - permissive licenses, directly relevant to your stack

## Why This Topic Matters (Career Angle)

- Contributing to open source (even small fixes to pytest plugins, Selenium wrappers, or test utilities) is high-signal proof for SDET/QA roles - it shows you can read unfamiliar code, write tests, and follow contribution standards.
- Understanding license types matters if you ever pick dependencies for a company project - using a GPL library inside proprietary software can create legal exposure.

## Further Reading

- [opensource.org/osd](https://opensource.org/osd) - the official Open Source Definition
- [choosealicense.com](https://choosealicense.com) - plain-English comparison of common licenses
- Search: "MIT vs GPL license difference" for a fast practical comparison

## Self-Check Questions

1. Does "open source" require the software to be free of cost? Why or why not?
2. What's the practical difference between a permissive and a copyleft license?
3. How is open source different from public domain?
