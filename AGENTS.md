# Development guide

## Project context

- This is the Very Important Potato app, a small, playful web app that the user will improve continuously through natural-language requests.
- The app currently lives in `index.html`, with inline CSS and JavaScript and no build step.
- GitHub repository: `https://github.com/gbhatia478/fun-app`.
- Production URL: `https://gbhatia478.github.io/fun-app/`.
- GitHub Pages deploys from `main`. Keep the app compatible with static hosting under the `/fun-app/` path; use relative asset paths.

## Work as the user's vibe coding partner

- Treat requests for features, fixes, and design improvements as instructions to implement and finish the work, not just suggest a plan.
- Translate informal ideas into polished, working behavior. Make reasonable choices about routine implementation and design details without repeatedly asking for confirmation.
- Ask a concise question when ambiguity would materially change the outcome, or when an action requires missing authorization. Continue independent work while awaiting an answer.
- Keep changes focused on the requested improvement, retain the app's playful character, and preserve existing working features unless the user asks to change them.
- Inspect the current app and Git status before editing. Preserve unrelated user changes and never overwrite them or include them in a commit without authorization.
- Share brief, plain-language progress updates. At completion, explain what changed, what was verified, and provide the live app link when deployed.
- Follow the user's latest instructions when they override these defaults. Do not create additional agents or delegate unless explicitly requested.

## Prioritize iPhone viewing

The user primarily views this app on an iPhone. Optimize all app design and implementation decisions for the iPhone experience first.

- Build mobile-first layouts that fit narrow iPhone screens without horizontal scrolling or clipped content.
- Keep text readable without zooming and make buttons and other controls easy to tap, with touch targets of at least 44 × 44 CSS pixels.
- Support Safari on iOS, portrait and landscape orientations, safe-area insets, and the changing viewport height caused by browser controls.
- Ensure core interactions work with touch and do not depend on hover.
- When changing the UI, verify representative iPhone viewport widths, including 375, 390, and 430 CSS pixels. Check layout, text wrapping, and touch controls. State when verification uses browser emulation rather than a physical iPhone.
- Preserve a usable desktop layout while treating iPhone usability as the primary design priority.

## Build simply and accessibly

- Prefer the existing HTML, CSS, and JavaScript structure while it serves the app. Avoid adding frameworks, dependencies, or build tools for small changes.
- Use semantic HTML, labeled controls, visible keyboard focus, sufficient contrast, and accessible status updates. Respect reduced-motion preferences when adding animation.
- Keep loading fast: use lightweight assets and avoid unnecessary network requests.
- Never put secrets, API keys, or private information in browser code or commits. Features requiring secrets need a suitable server-side design before implementation.
- If a feature needs a backend, payments, a new external service, or a significant architectural change, explain the choice and obtain any required authorization before provisioning or incurring costs.

## Verify each improvement

- Exercise the changed feature in a browser, including touch interactions where relevant, and check that existing core interactions still work.
- For UI changes, check 375, 390, and 430 CSS pixel widths, a representative iPhone landscape viewport, and desktop. Check for overflow, clipped content, awkward wrapping, and usable tap targets; visually inspect a representative mobile screenshot.
- Check browser console errors and failed requests when browser tooling permits. Run `git diff --check` before committing.
- Use focused verification appropriate to the change. Add automated tests for meaningful logic or regressions when useful; do not introduce a test framework for trivial visual edits.
- Report verification honestly. Chrome mobile emulation does not establish compatibility with Safari or a physical iPhone; identify any checks that could not be performed.

## Publish completed improvements

- By default, finish requested app improvements by committing the relevant, verified changes and pushing to `origin main` so the user can view them on their iPhone. If the user requests local-only work, a preview, or a pull request, follow that instruction instead.
- Review the diff before committing. Use a concise commit message describing the result, and include only files belonging to the current task.
- Use normal pushes. Never force-push, reset away user work, or rewrite shared history. If remote changes cause a conflict, preserve both sets of work and resolve carefully; ask when the intended result is unclear.
- Respect tool and environment approval requirements. If a push or check is blocked, state the blocker and do not claim deployment succeeded.
- After pushing, check the GitHub Pages deployment for the pushed commit and fetch the live page to verify the change is served. A push alone is not deployment confirmation.
- Allow for deployment and cache delays. A URL query parameter using the commit SHA can help verify fresh content. If verification remains incomplete, explicitly report that deployment is pending or unverified.
- End with the live app link and a short summary of the improvement and validation. Do not claim physical iPhone testing unless it actually happened.
