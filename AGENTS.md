# Working agreement

Keep instructions focused on recurring failures. Put task-specific guidance in
`.agents/skills/` and keep project details in the adopting project's own files.

- Resolve the actual review comparison. `main...HEAD` omits uncommitted work on
  main; an empty branch diff does not mean the working tree was reviewed.
- Reuse existing test devices and build caches. Follow the project's storage
  budget rather than creating new devices or permanent caches for each task.
- Hold resource ownership through manual interaction as well as scripted runs.
  A busy resource does not authorize cancelling another task's process.
- Where a browser audit wrapper exists, use it with a managed test browser;
  preserve personal browser profiles and close only owned sessions.
- A successful push or commit is not approval to deploy, distribute, or change
  production, billing, IAM, signing or store settings. Existing approval covers
  only its authorized scope.
