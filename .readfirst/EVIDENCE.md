# Evidence for the readfirst map rules

The fill run stopped at its cost cap before it wrote evidence. Each rule below was checked by hand against the code at 6b463b4.

| Rule | Where the code keeps it |
|---|---|
| r2-delete-owned-keys-only | `apps/web/lib/api/links/get-owned-link-image-key.ts:15`, used in `delete-link.ts:26` and `bulk-delete-links.ts:57` |
| bulk-delete-one-workspace | `apps/web/lib/api/links/bulk-delete-links.ts:19-20` (stated in the comment), `:72` (`links[0].projectId`) |
| user-urls-via-safe-fetch | `apps/web/lib/api/safe-fetch.ts`, `safe-fetch-node.ts`, `is-private-ip.ts`; used in `lib/sitemaps/import-tracked-sitemaps.ts`, `lib/storage.ts`, `app/api/links/metatags/utils.ts` |
| routes-declare-permissions | `apps/web/lib/auth/workspace.ts:69-75` (option), `:459` (enforced only when the list is non-empty) |
| actions-check-permissions | 15 actions use `authActionClient`; the 4 without a role check change only the caller's own preferences or verify folder access (`create-oauth-url.ts`, `set-default-folder.ts`) |
| stripe-raw-body-before-parse | `apps/web/app/(ee)/api/stripe/webhook/route.ts:32` (`req.text()`), `:40` (`constructEvent`) |
| jobs-registered-by-name | `apps/web/lib/jobs/registry.ts:3` (convention), `:6-20` (keys equal job names) |
| webhook-signature-json-body | `apps/web/lib/webhook/signature.ts:2-18` (HMAC-SHA256), `qstash.ts:90` (signs the payload that is sent) |
| hubspot-component-layout | `packages/hubspot-app/src/app/app-hsmeta.json:24` (`permittedUrls`) |
| link-writes-stay-in-step | `create-link.ts:54,143,146`; `update-link.ts:82,179,182,185`; `delete-link.ts:20,34,37` |

`link-writes-stay-in-step` was dropped by the run because it cited a line that does not exist (`lib/middleware/link.ts:88`); it is added back here with the lines above.
