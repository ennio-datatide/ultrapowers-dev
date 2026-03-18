---
name: Supabase Patterns
description: "Use when building with Supabase. Covers row-level security, realtime subscriptions, edge functions, auth, and PostgreSQL best practices within the Supabase platform."
---

# Supabase Patterns

Supabase is PostgreSQL with batteries: auth, realtime, storage, and edge functions. Security lives in the database via Row-Level Security -- if RLS is off, your data is public.

## Row-Level Security (RLS)

- **Enable RLS on every table** exposed via the API: `ALTER TABLE posts ENABLE ROW LEVEL SECURITY;`.
- **Deny by default.** With RLS enabled and no policies, all access is blocked. Add policies explicitly.
- **Use `auth.uid()`** in policies to scope access to the authenticated user:
  ```sql
  CREATE POLICY "Users see own posts" ON posts
    FOR SELECT USING (user_id = auth.uid());
  ```
- **Separate policies per operation:** SELECT, INSERT, UPDATE, DELETE each need their own policy.
- **Test policies** by switching roles: `SET ROLE authenticated; SET request.jwt.claims = '{"sub":"user-id"}';`.

## Auth

- **Use `@supabase/ssr`** for Next.js or `@supabase/auth-helpers-*` for other frameworks.
- **Server-side client** (`createServerClient()`) reads cookies and validates JWT automatically.
- **Never trust the client JWT alone** -- RLS policies are the real enforcement layer.
- **Custom claims** via `raw_app_meta_data` for role-based access.

## Realtime Subscriptions

- **Enable realtime per table** in the Supabase dashboard or via `ALTER PUBLICATION supabase_realtime ADD TABLE posts;`.
- **Subscribe in client:**
  ```typescript
  supabase.channel('posts').on('postgres_changes',
    { event: 'INSERT', schema: 'public', table: 'posts' },
    (payload) => handleNew(payload.new)
  ).subscribe();
  ```
- **RLS applies to realtime** -- users only receive events for rows they can SELECT.
- **Unsubscribe on cleanup** to avoid memory leaks: `supabase.removeChannel(channel)`.

## Edge Functions

- **Deno-based** serverless functions deployed to Supabase's edge network.
- Use for webhooks, third-party API calls, and server-only logic.
- **Create with:** `supabase functions new my-function`, deploy with `supabase functions deploy`.
- **Service role key bypasses RLS** -- use only in trusted server contexts, never expose to clients.

## PostgreSQL Best Practices (Supabase Context)

- **Use migrations** via `supabase migration new` -- never modify production schemas manually.
- **Foreign keys with cascading deletes** where appropriate: `REFERENCES users(id) ON DELETE CASCADE`.
- **Indexes on filtered/joined columns** -- check with `EXPLAIN ANALYZE` in the SQL editor.
- **Database functions** for complex logic: `CREATE FUNCTION` keeps business rules in the database, callable via `supabase.rpc()`.

## Common Pitfalls

| Pitfall | Fix |
|---|---|
| RLS disabled on public tables | Enable RLS immediately; add policies before exposing via API |
| Using `service_role` key in client code | Client must use `anon` key; service role bypasses all security |
| Missing realtime publication for table | Add table to `supabase_realtime` publication |
| Not unsubscribing from channels | Clean up in `useEffect` return or component unmount |
| Running migrations only via dashboard | Use `supabase migration new` for version-controlled, repeatable schema changes |

## Attribution
**Original** -- Datatide, MIT licensed. See also [supabase/agent-skills](https://github.com/supabase/agent-skills) for official Supabase skills.
