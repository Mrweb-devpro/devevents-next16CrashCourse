<wizard-report>
# PostHog post-wizard report

The wizard has completed a deep integration of PostHog analytics into the Dev Events Next.js app. Here's a summary of all changes made:

- **`instrumentation-client.ts`** (created): Initializes PostHog client-side using the Next.js 15.3+ instrumentation API. Configured with a reverse proxy host (`/ingest`), exception capture enabled, and debug mode in development.
- **`next.config.ts`** (updated): Added reverse proxy rewrites routing `/ingest/*` traffic to PostHog's US ingestion endpoint, plus `skipTrailingSlashRedirect: true` for PostHog API compatibility.
- **`components/ExploreBtn.tsx`** (updated): Added `posthog.capture('explore_events_clicked')` to the existing `onClick` handler.
- **`components/EventCard.tsx`** (updated): Added `"use client"` directive and `posthog.capture('event_card_clicked', { title, slug, location, date })` on the card link click.
- **`components/Navbar.tsx`** (updated): Added `"use client"` directive and `posthog.capture('nav_link_clicked', { label })` on each navigation link.
- **`.env.local`** (created): PostHog public token and host stored as environment variables (`NEXT_PUBLIC_POSTHOG_KEY`, `NEXT_PUBLIC_POSTHOG_HOST`).

## Events

| Event name | Description | File |
|---|---|---|
| `explore_events_clicked` | User clicks the 'Explore Events' CTA button on the homepage hero | `components/ExploreBtn.tsx` |
| `event_card_clicked` | User clicks on an event card to view details — top of discovery funnel | `components/EventCard.tsx` |
| `nav_link_clicked` | User clicks a navigation link in the top navbar | `components/Navbar.tsx` |

## Next steps

We've built some insights and a dashboard for you to keep an eye on user behavior, based on the events we just instrumented:

- **Dashboard — Analytics basics**: https://us.posthog.com/project/392886/dashboard/1497726
- **Insight — Explore Events button clicks**: https://us.posthog.com/project/392886/insights/kMwlLNGu
- **Insight — Total event card clicks**: https://us.posthog.com/project/392886/insights/IXWIQv3C
- **Insight — Event card clicks by event title**: https://us.posthog.com/project/392886/insights/i5Z11HQp
- **Insight — Discovery funnel: Hero CTA → Event card**: https://us.posthog.com/project/392886/insights/siWwAxuI
- **Insight — Nav link clicks by label**: https://us.posthog.com/project/392886/insights/6A4HJdKU

### Agent skill

We've left an agent skill folder in your project. You can use this context for further agent development when using Claude Code. This will help ensure the model provides the most up-to-date approaches for integrating PostHog.

</wizard-report>
