# Oakland Track Club website

Static rebuild of https://www.oaklandtrackclub.org, migrated off Wix in October 2026.
It's plain HTML and CSS, with a tiny bit of JavaScript. There's no build step, no CMS, and no dependencies.

## Structure

```
index.html                  Home
about/index.html            Our story
weekly-runs/index.html      Weekly runs schedule
otc-events/index.html       Events (Summer Classic, Winter Classic, Lake Merritthon)
membership/index.html       Contact and Membership
contact/index.html          Contact (not in the main nav, same as on Wix)
404.html                    Not-found page
css/style.css               All styles. Colors and fonts are variables at the top.
js/main.js                  Header hide-on-scroll, mobile menu, Instagram feed, home-page lightbox
images/                     All images

copy-of-about/              Redirect from the old Wix URL to /weekly-runs/
pricing-plans/membership/   Redirect from the old Wix URL to /membership/
```

## Editing

- **Text:** open the page's `index.html` and edit the text directly.
- **Weekly runs:** each run is an `<article class="run">` block in `weekly-runs/index.html`.
  To add a run, copy a block. To remove one, delete its block.
- **Events:** each event is an `<article class="event">` block in `otc-events/index.html`. When registration opens,
  swap the `<span class="btn ...">Check back next year</span>` for a link:
  `<a class="btn btn--italic" href="https://...">Register now</a>`.
- **Images:** add the file to `images/` and reference it as `images/name.jpg` from the home page, or
  `../images/name.jpg` from pages inside a folder. Keep photos at about 2400px wide or smaller.
- **Header and footer:** these are copied into every page. If you change the nav or footer, update all 6 pages
  plus `404.html`.

## Instagram feed (footer)

Instagram doesn't offer a public feed that a static site can read, so the footer feed uses
[Behold](https://behold.so). Its free plan converts the club's Instagram into a JSON feed and refreshes it automatically.

1. Sign up at behold.so and connect the @oaklandtrackclub Instagram account.
2. Create a feed and copy its **JSON feed URL**. It looks like `https://feeds.behold.so/AbC123xyz`.
3. Paste it into `INSTAGRAM_FEED_URL` at the top of `js/main.js`.

Until a URL is set, or if the feed can't load, the footer shows only a "Follow @oaklandtrackclub on Instagram" link.

## Header behavior

The header is a fixed, semi-transparent bar. It slides up out of view when you scroll down and comes back when you
scroll up. The logic is in `js/main.js`, and the styles are under "Header / Nav" in `css/style.css`.

## Preview locally

```bash
python3 -m http.server 8000
```

Then open http://localhost:8000.

## Deploying

Any static host works. There's no build command, and the publish directory is the repository root.

- **GitHub Pages:** push to GitHub, go to Settings → Pages, and choose "Deploy from a branch" (`main`, `/ (root)`).
  Add a `CNAME` file containing `www.oaklandtrackclub.org` for the custom domain.
- **Netlify:** use "Add new site" → import the repo. Leave the build command empty and set the publish directory to `/`.
- **Vercel:** import the repo with the framework preset "Other" and no build command.

When you point the domain away from Wix, update the DNS records at your registrar as your host instructs.
If the domain is registered through Wix, transfer it out before the Wix plan expires.

## Not carried over from Wix

- The online store (`/product-page/*`). It wasn't linked from the site.
- The Wix Events pages (`/event-details-registration/*`). These were all 2022–2023 events.
- The blog. Its only post was Wix placeholder text.
- Pricing-plan checkout. The live site showed "No plans available". Membership is handled by email.
- The Wix Instagram feed app. It's replaced by the Behold-powered footer feed described above.
