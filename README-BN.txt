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