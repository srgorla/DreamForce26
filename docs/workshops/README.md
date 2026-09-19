# Workshop index

Each workshop has a student guide and an exercise guide. Keep both links in
`docs/workshops/<workshop-name>/README.md`, alongside task progress and notes.

| Workshop | Guides and notes | Branch | Status |
| --- | --- | --- | --- |
| Agentforce Service Assistant (Dynamic Plans) | [Workshop reference](service-assistant-dynamic-plans/README.md) | `workshop/service-assistant-dynamic-plans` | In progress |

## Adding a workshop

1. Create `workshop/<workshop-name>` from `main`.
2. Create `docs/workshops/<workshop-name>/README.md` with the workshop title,
   student guide URL, exercise guide URL, branch, target org alias, and links to
   progress and implementation notes. Mark unavailable guide links as pending.
3. Add a row to this index.
4. Track each task and its validation in the workshop folder and create a
   separate commit for each task.
5. When the workshop is complete and verified, update its status and merge
   into `main`, preserving the task commits.

Keep credentials and authentication files out of workshop documentation.
