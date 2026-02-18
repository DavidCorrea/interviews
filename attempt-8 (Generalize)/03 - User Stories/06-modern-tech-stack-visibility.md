# User Story: Modern Tech Stack Visibility

**Priority:** Medium  
**Related Finding:** [Finding 6](../main-report.md#finding-6)

## Story
As a technical founder evaluating agencies, I want to see the full breadth of modern technologies the agency works with, so that I can confirm they can build with the stack I prefer.

## Context
The Technologies page lists Ruby on Rails, ReactJS, and Ionic as the primary frameworks. While solid, these don't reflect the modern startup tech ecosystem (Next.js, TypeScript, Tailwind, Vercel, Supabase). The agency claims to be "tech-agnostic" but the limited technology listing creates a perception that they're behind the curve on modern tooling.

## Acceptance Criteria
- The Technologies page lists modern frameworks alongside existing ones (Next.js, TypeScript, Tailwind CSS, Node.js, etc.)
- If the agency truly uses these technologies, they should be listed with the same depth as Rails and React
- The "tech-agnostic" claim is supported by visible diversity in listed technologies
- The page structure groups technologies by capability (Frontend, Backend, Mobile, AI, Infrastructure) rather than leading with vendor-specific products

## How to Test
1. Navigate to the Technologies page
2. Verify at least 3 modern frameworks/tools are listed (e.g., Next.js, TypeScript, Node.js, Tailwind)
3. Confirm technologies are grouped by capability, not vendor
4. Ask a frontend developer to review the page and confirm the listed stack feels current

## Developer Notes

### General Approach
Update the Technologies page content to include additional frameworks and tools the team actually works with. Restructure the page to lead with capability categories rather than vendor platforms.

### Components to Audit
- Technologies page content/layout
- Technology card/list component
- CMS entries for technology descriptions

### Code Examples
```jsx
const techCategories = [
  {
    name: "Frontend",
    technologies: [
      { name: "React", description: "Component-based UI library" },
      { name: "Next.js", description: "Full-stack React framework with SSR" },
      { name: "TypeScript", description: "Type-safe JavaScript" },
      { name: "Tailwind CSS", description: "Utility-first CSS framework" },
    ]
  },
  {
    name: "Backend",
    technologies: [
      { name: "Ruby on Rails", description: "Rapid web app development" },
      { name: "Node.js", description: "JavaScript runtime for server-side" },
      { name: "Python", description: "AI/ML and backend services" },
    ]
  },
  {
    name: "Mobile",
    technologies: [
      { name: "React Native", description: "Cross-platform mobile with React" },
      { name: "Ionic", description: "Hybrid mobile framework" },
      { name: "Flutter", description: "Google's cross-platform UI toolkit" },
    ]
  },
  {
    name: "AI & ML",
    technologies: [
      { name: "OpenAI / GPT", description: "Large language model integration" },
      { name: "LangChain", description: "LLM application framework" },
      { name: "Custom ML", description: "Bespoke machine learning models" },
    ]
  },
];
```

## How Other Sites Achieve This
- **Vercel** — clearly shows their framework ecosystem (Next.js, SvelteKit, Nuxt, etc.) organized by type
- **Netlify** — groups technologies by use case (frontend, backend, CMS, etc.)
- **Thoughtbot** — lists all technologies they use with equal visual weight, organized by type
