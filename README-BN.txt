# নবীগঞ্জ ভিউ | Nabiganj View

বাংলা ও ইংরেজি সংবাদ পোর্টাল। Frontend: HTML/CSS/JavaScript; Backend: Supabase.

## প্রকাশনা
- index.html: Public news portal
- admin.html: Admin login and pending-news moderation
- Hosting: Render Static Site (publish directory: .)

## Supabase
Project URL: https://nywlrdazdcybidlmfnmj.supabase.co
Browser key: Publishable key (safe to expose with correct RLS policies).
Never put service_role key, collector secret, or Gemini API key in frontend files.

## Admin access
Create an Auth user in Supabase, then securely assign app_metadata.role = admin using a trusted server-side/admin process. Do not put admin credentials in this repository.

## Notes
The public portal shows short summaries, source attribution, and links to original publishers. It does not republish full copyrighted articles. Check Supabase RLS and foreign-key relationships before production use.

## নতুন newsroom সুবিধা (2026-11-04)
- admin.html: মোবাইল-ফ্রেন্ডলি newsroom dashboard, article create/edit, draft/pending/scheduled/published, category/location, SEO metadata, featured/breaking flags, image upload.
- article.html: published article detail, sanitized article body, source attribution, share links, moderated comments and comment reports.
- AI editor assistant: authenticated Supabase Edge Function; Bengali/English headline, summary and translation assistance. Human editorial review remains required.
- breaking_news: admin-controlled breaking ticker.
- comments / comment_reports: pending-first comment moderation.
- advertisements: banner placements; publisher code stored in admin-only ad_network_configs table (not exposed to public clients).
- article_revisions and admin_audit_logs: article revision snapshots and status-change audit entries.
- page_views: page view tracking; view_count is updated by database trigger.
- Storage bucket: news-media (public read, newsroom upload restrictions).
- scheduled articles: database cron publishes due scheduled stories when a summary exists.
- robots.txt and initial sitemap.xml.

## Newsroom roles
Roles are assigned only through trusted Supabase Auth app_metadata (never user_metadata):
- super_admin: full access including advertising and site settings.
- admin: newsroom administration and user management permissions where implemented.
- editor: edit, publish, breaking ticker, comments and newsroom operations.
- reporter: create and edit own stories, upload media, use AI editor.
- moderator: comment/report moderation.
The existing login user must have app_metadata.role set to an allowed role. Refresh or sign out/in after changing app_metadata.

## Important production notes
- The public article detail page uses article.html?id=<article UUID>. Existing imported articles without body_html show the original AI summary; readers can open the attributed original source.
- AI generation is assistive only; it does not verify truth or replace human fact-checking.
- RSS collection and AI summarization cron jobs remain active. Do not publish unreviewed allegations; verify names, dates, locations and claims.
- Comments are pending by default. Add CAPTCHA / rate limiting before a large public launch.
- Publisher scripts are kept private and are not executed automatically. Verify network policies and consent requirements before enabling ad code.
- Sitemap is a static initial sitemap and needs ongoing automation or periodic regeneration as new articles publish.
- SEO tags and NewsArticle structured data are present on the article page, but full server-rendered social previews for query-string article pages require a server-side rendering or edge rewrite layer.
- Enable Supabase Auth leaked-password protection in the dashboard before public launch.
- Never place service-role keys, Gemini API keys, collector secrets, or admin passwords in frontend files or GitHub.
