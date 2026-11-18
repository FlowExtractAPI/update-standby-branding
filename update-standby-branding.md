# Update Standby branding to Server Actors

Rewrites any README (or markdown file) that mentions "Standby" to follow the Server Actors naming guidelines, or adds a Server Actors section if the README has no Standby mentions at all. Apply every rule below; leave code-level identifiers (env vars, `actor.json` keys, code comments) unchanged.

## Argument

$ARGUMENTS - Path to the markdown file(s) to update. If empty, search the current directory tree for README files that mention "Standby" (case-insensitive) and list them for the user to confirm before editing.

## Naming rules

These come from the Server Actors Naming One-pager and are authoritative.

### Term definitions

| Term | What it means | Where to use it | Capitalization |
|---|---|---|---|
| **Actor** | The Apify building block | Everywhere | Always capitalized |
| **Server Actor(s)** | An Actor with the server interface enabled | Headlines, changelog, Store badge, sales collateral, blog, conversation, section headings | Both words capitalized (it's a name) |
| **server interface** | The HTTP mechanism an Actor exposes | Docs prose, `actor.json`, API fields, mechanics explanations | Always lowercase |
| **input interface** | The classic run-with-input mechanism | Only where both interfaces are named together | Always lowercase |
| **multi-tenant** / **single-tenant** | Tenancy of a Server Actor | Docs prose, Console settings | Lowercase and hyphenated in prose. Console labels start capitalized (match the UI) |

### Before-and-after replacements

Apply these substitutions contextually (not as blind find-replace):

| Before (old) | After (new) | Context |
|---|---|---|
| Actor Standby mode (feature name) | Server Actors | "Introducing Server Actors" |
| Standby mode / Server mode | server interface | "Call the server interface over HTTP" |
| Standby Actor / Actor in Standby mode | Server Actor | "A Server Actor answers HTTP requests as they come in" |
| Standby web server | server interface (prose) or Server Actors (heading) | Depends on context |
| Standby Actor URL | server interface URL | "Get the server interface URL" |
| started in Standby | which interface started the Actor | "Check which interface started the Actor" |
| Monetization of Actors in Standby mode | Monetizing Server Actors | Heading or feature context |
| Normal Actor run / normal mode | Actor run (via input interface) | When contrasting with server interface |
| Normal run output | Run output | Simplified heading |
| Actor server / Actor with Server interface | Server Actor | "Build a Server Actor" |
| multi-tenant Server (capitalized) | multi-tenant Server Actor | The tenancy describes a Server Actor |
| Standby requests | Server Actor requests / requests via the server interface | Depends on context |

### Do's and don'ts

| Term | Do | Don't |
|---|---|---|
| Actor | "Call this Actor over HTTP" | "Call this actor over HTTP" |
| Server Actors | "Build real-time experiences with Server Actors" | "server Actors", "Server actors" |
| server interface | "Get the server interface URL" | "Server interface URL", "Server Interface URL" |
| input interface | "Start a run with the input interface" | "Input Interface", "Input interface" |
| multi-tenant | "Switch your Server Actor to multi-tenant" | "Multi-tenant" (in prose), "multitenant" |
| First mention (docs/blog) | "Server Actors (formerly Actor Standby mode)" | "Server Actors (Standby)", "Server Actors (formerly Standby Actors)" |

### What NOT to change

- **Code-level identifiers**: `APIFY_META_ORIGIN=STANDBY`, `standby` in `actor.json` keys, env vars, code blocks showing config - these stay as-is. The one-pager says "`standby` stays as the code name for now in the codebase."
- **Links to docs**: Update the URL path if the docs have moved (e.g. `/actors/running/standby` -> `/actors/running/server-actors`), but only if the new URL is provided or confirmed.
- **Other files**: This skill targets markdown/README files only.

## Workflow

1. **Find files**: If no path was given, search for README files mentioning "Standby" (case-insensitive, excluding code blocks). List them and ask the user to confirm.
2. **Read the file**: Read the full markdown file.
3. **Identify all Standby mentions**: Grep for "Standby" (case-insensitive). Classify each as:
   - **Content** (prose, headings, link text) - these get updated
   - **Code** (fenced code blocks, inline code, env vars) - these stay unchanged
   - **URLs** (href targets) - flag for the user to verify if the target has moved
4. **Branch based on Standby presence**:
   - **If Standby mentions exist** -> continue to step 5 (replacement flow).
   - **If no Standby mentions exist** -> jump to step 9 (Server Actor insertion flow).

### Replacement flow (README already mentions Standby)

5. **Apply replacements**: Use the before-and-after table above. Choose "Server Actors" vs "server interface" based on context:
   - Headings, feature introductions, product references -> **Server Actors**
   - Mechanics prose, technical explanations, API references -> **server interface**
6. **Add transition callout**: On the first mention of "Server Actors" in the document, append "(formerly Actor Standby mode)" if not already present.
7. **Verify capitalization**: Check every instance of Actor (capitalized), Server Actor(s) (both capitalized), server interface (both lowercase), input interface (both lowercase), multi-tenant/single-tenant (lowercase, hyphenated).
8. **Show the diff and write**: Present the changes to the user before writing. Apply the changes after user confirmation. Skip to Output.

### Insertion flow (README has no Standby mentions)

When the README never mentions Standby, add a short Server Actors section so users discover the server interface as an alternative way to call the Actor.

9. **Locate the insertion point**: Find the section about results volume, limitations, or benchmarks (e.g. "How many results can you scrape with …"). The new section goes **directly after** that section. If no such section exists, insert it **before the Integrations section**, or before the API usage section as a fallback.
10. **Ask the user** to confirm the insertion point and whether they want any adjustments to the template below.
11. **Insert the Server Actor section** using this template (adapt the Actor name, slug, and use-case description to match the README):

```markdown
## Is this Actor available as a Server Actor?

This Actor is also available via the [server interface](https://docs.apify.com/platform/actors/running/server-actors). Instead of starting a full run and waiting for results, you can send a single HTTP request and get the data back in the response — perfect for checking individual URLs in real time.

To call this Actor via the server interface:

1. Send an HTTP request to the server interface URL with your input as the request body.
2. Receive the results directly in the HTTP response.

This is ideal when you need to look up a single place or a small number of URLs on demand, without managing full scraping runs.
```

12. **Verify capitalization** of the inserted text: Actor (capitalized), Server Actor (both capitalized), server interface (both lowercase).
13. **Show the diff and write**: Present the changes to the user before writing. Apply the changes after user confirmation.

## Output

### After replacements (Standby was present)

Provide a summary table:

| Change | Count | Example |
|---|---|---|
| "Standby mode" -> "server interface" | N | Line X: ... |
| "Standby web server" -> "Server Actors" | N | Line X: ... |
| ... | ... | ... |
| Skipped (code/env var) | N | Line X: `APIFY_META_ORIGIN=STANDBY` |

### After insertion (no Standby was present)

Provide a summary:

| Action | Detail |
|---|---|
| Inserted section | "Is this Actor available as a Server Actor?" |
| Insertion point | After "How many results…" / Before "Integrations" |
| Lines added | N |
