# Development guide

## Project context

- This is Samit Dodges Responsibility, a playful side-scrolling survival game that grew out of the Very Important Potato app. The user will improve it continuously through natural-language requests.
- The app currently lives in `index.html`, with inline CSS and JavaScript and no build step.
- GitHub repository: `https://github.com/gbhatia478/fun-app`.
- Production URL: `https://gbhatia478.github.io/fun-app/`.
- GitHub Pages deploys from `main`. Keep the app compatible with static hosting under the `/fun-app/` path; use relative asset paths.

## Game purpose and difficulty

- Samit automatically runs while responsibilities such as meetings, deadlines, and chores approach. Players time jumps to avoid them, survive, and compete on the shared leaderboard.
- Make the game easy to learn and difficult to master. The humor and costume unlocks support the game; the core challenge is precise jump timing as obstacles become harder.
- Scores currently increase by one point per second of active play. Keep displayed scores and existing leaderboard entries on a consistent scale when changing scoring.
- Points 1–10 are a forgiving learning phase. Difficulty increases smoothly after 10, reaches about 75% of the ramp at 30, and reaches full difficulty at 50. These are the current design targets; follow later user adjustments.
- Around 30 points, play should feel demanding and require near-perfect timing. At 50 and beyond, the intent is to require almost perfect play. High scores should reflect skill and consistency.
- Increase challenge through obstacle speed, spacing, and height. Taller obstacles should require clearing them near the top of a jump. Keep visible obstacles and collision rules consistent.
- Keep the challenge fair: preserve enough time to land and jump again, avoid impossible obstacle sequences, and check precise play at both 30 and 60 fps on representative iPhone sizes. Simulated survival proves playability, but human playtesting determines whether the difficulty feels right.

## Work as the user's vibe coding partner

- Treat requests for features, fixes, and design improvements as instructions to implement and finish the work, not just suggest a plan.
- Translate informal ideas into polished, working behavior. State assumptions and surface uncertainty before implementing; follow the principles below rather than silently choosing an interpretation.
- Ask concise clarifying questions before implementing unclear requirements. Pause work that depends on the answer; continue independent work where possible. Do not repeatedly ask for authorization already provided.
- Keep changes focused on the requested improvement, retain the app's playful character, and preserve existing working features unless the user asks to change them.
- Inspect the current app and Git status before editing. Preserve unrelated user changes and never overwrite them or include them in a commit without authorization.
- Share brief, plain-language progress updates. At completion, explain what changed, what was verified, and provide the live app link when deployed.
- Follow the user's latest instructions when they override these defaults. Do not create additional agents or delegate unless explicitly requested.

## 1. Think before coding

Don't assume. Don't hide confusion. Surface tradeoffs.

Before implementing:

- State assumptions explicitly. If uncertain, ask.
- If multiple interpretations exist, present them; don't pick silently.
- If a simpler approach exists, say so. Push back when warranted.
- If something is unclear, stop the affected work, name what's confusing, and ask.

## 2. Simplicity first

Write the minimum code that solves the problem. Nothing speculative.

- No features beyond what was asked.
- No abstractions for single-use code.
- No flexibility or configurability that wasn't requested.
- No error handling for impossible scenarios.
- If 200 lines could be 50, rewrite the solution more simply.
- Ask: "Would a senior engineer say this is overcomplicated?" If yes, simplify.

## 3. Surgical changes

Touch only what you must. Clean up only your own mess.

When editing existing code:

- Don't improve adjacent code, comments, or formatting outside the request.
- Don't refactor things that aren't broken.
- Match the existing style, even if you'd do it differently.
- If you notice unrelated dead code, mention it; don't delete it.
- Remove imports, variables, and functions that your changes made unused.
- Don't remove pre-existing dead code unless asked.
- Every changed line should trace directly to the user's request.

## 4. Goal-driven execution

Define success criteria. Loop until verified.

Transform tasks into verifiable goals:

- "Add validation": write tests for invalid inputs, then make them pass.
- "Fix the bug": reproduce it with a focused test, then make it pass.
- "Refactor X": ensure relevant tests pass before and after.

Use the focused verification guidance below to choose an appropriate test or browser check without introducing unnecessary testing infrastructure.

For multi-step tasks, state a brief plan with a check for each step:

1. [Step] → verify: [check]
2. [Step] → verify: [check]
3. [Step] → verify: [check]

Strong success criteria enable independent execution. Clarify vague goals before implementing. Continue until the criteria are verified or a concrete blocker requires user input; report any remaining gap honestly.

These principles are working when diffs contain fewer unnecessary changes, solutions need fewer rewrites due to overcomplication, and clarifying questions come before implementation rather than after mistakes.

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
