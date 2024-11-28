---
title: "Rewriting my blog with AI"
description: "I used AI to swap blog platforms. Here's how it went."
pubDatetime: 2024-11-27T11:00:00-7:00
---

I've been blogging for a few years. I started with Wordpress, then moved to Jekyll for a while. I experimented with Ghost and ultimately scrapped it. Anyway, it's a been a long time and it was overdue since I was still using the base Jekyll installation. 

You can see the starting point here:

<img src="/assets/ai-blog/blog-home.png" alt="Blog homepage and post list" />
<img src="/assets/ai-blog/blog-post.png" alt="Blog post" />

So given that it was time to rewrite, I wanted to try something new. I determined Astro is basically what I wanted to use and looked into the swap.

### What I would've done traditionally

Traditionally, I would've relied upon blog posts and the like to help me to do the migration. These are two well-known platforms, so they should have an easy migration path. While the official Astro site [has a guide](https://docs.astro.build/en/guides/migrate-to-astro/from-jekyll/) for migrating, it basically has a ["draw the owl"](https://xkcd.com/927/) approach. For example:

> Much of your existing HTML page content can be converted into Astro pages

> Astro does not have a permalink property that accepts placeholders. You may need to read more about Astro’s page routing if you want to keep your existing URL structure. Or, consider setting redirects at a host like Netlify.

So yeah, it would work, but I have to rewrite all the URLs as well as migrate the content formatting.

There's other guides as well, like [this
one](https://www.kooslooijesteijn.net/blog/jekyll-or-astro-which-is-better-static-site-generator),
which goes into depth about the trade-offs and how to migrate, and [Creating a
Jekyll-style blog post URL in
Astro](https://humanwhocodes.com/blog/2023/03/astro-jekyll-blog-post-url/) which
goes into the details of how to migrate the URLs specifically (there's also [a
package they made for this: [astro-jekyll](https://github.com/humanwhocodes/astro-jekyll)]). 

But, you're still pretty much on your own to do the migration.

### What I did with AI

I've been following AI and using it at work pretty heavily. My experience has mostly been with using OpenAI / Claude for high-level discussions with GitHub Copilot for auto-fill & back and forth iteration in chat. Notably, with Github Copilot, you're still needed in the loop to go back and forth with it, and it's pretty slow in IntelliJ from my experience (both in terms of how it generates and the delay until it starts generating), I've been able to do a lot of the work in the editor.

There's been some interest in the [r/ChatGPTcoding](https://www.reddit.com/r/ChatGPTcoding/) subreddit about using AI to write code. I thought I'd give it a shot and see how it goes.

The two main things I tried were:
1. [Aider](https://www.aider.chat/)
2. [Cursor](https://www.cursor.com/)


### Using Aider

So I subscribed to Claude, since most folks view Claude 3.5 as one of the better options out there at the moment.

I asked Aider to rewrite the blog platform to use Astro instead of Jekyll. While it did a lot of activity, I can't say I was impressed. 

I had a homepage that looked like this:

<img src="/assets/ai-blog/aider-homepage.png" alt="Aider homepage" />

It kept asking me to run npm run dev in-process, which was a blocking operation

I basically had no input while it was running. I was just a spectator. 

Actually, let me just show you the basic experience of Aider.

<figure>
    <iframe 
        width="560" 
        height="315" 
        src="https://www.youtube.com/embed/8-lzzK6dRAU" 
        title="Demo of Aider attempting blog migration"
        loading="lazy"
        allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture"
        allowfullscreen
        aria-label="Video demonstration of Aider migration attempt">
    </iframe>
    <figcaption>Demonstration of Aider attempting the initial migration</figcaption>
</figure>

It may be a little hard to see what's happening here. I asked it to generate a index of posts for the homepage. It generated some changes, applied them to ... files? And then asked me if I wanted to use Jekyll to serve them (no thank you). After responding a few more times, it ended and I was left with my homepage as it was. 

So maybe this is on me. Maybe AI tooling isn't quite there for this kind of migration.

#### Round 2

So, I followed the [Astro tutorial](https://docs.astro.build/en/getting-started/) and got a basic demo site running, and then came back to start the migration from a better starting point.

This time, I scaffolded the site with a bootstrap template (`npm create astro@latest -- --template satnaing/astro-paper`), moved the posts over into the `content/blog` folder, and started from there.

Immediate problems:
1. The expected fields for every post are different. In particular, I needed to add `pubDatetime` and `description`.
2. The url structure is different. Instead of `YYYY/MM/DD/title.html`, it's `YYYY-MM-DD-title.html`, which would break the links and any SEO value I might have had.

While I could do these things, it seems like there's probably an opportunity to use AI. I went back to try Aider again.

### Using Aider (again)

So I fed all the files into Aider and asked it to add a `pubDatetime` and
description, based on the post content and original datetimes.  It seems like AI
should be able to do that effectively, right?

Here's a video:

<iframe width="560" height="315" src="https://www.youtube.com/embed/q8q_DWUOCA8?si=4kBtY0LP2n8_IK6Y" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>

Nope. It sort of works, it sort of provides a starting point, but I have to manually provide every blog post every time, and there's 50+ posts, so that's not going to work great. I instead tried providing every post at once, or at least as many as I could, and it still didn't work **but** it charged me $0.25 per attempt because it was passing all of the context of all of the files to Claude.

After about an hour and $10 in credits, 
And this [awful commit history](https://github.com/kevinlondon/kevinlondon.github.io/commits/klondon/aider-commits/):

<img src="/assets/ai-blog/aider-commit-history.png" alt="Aider commit history" />


At this point, I gave up on Aider and started using Cursor.


I would like to say again that it's more likely I'm not using Aider correctly, or this may not be the right usecase for it. Lots of folks like Aider, I just had a bad experience this time.

### Using Cursor

I switched to Cursor and had a good experience almost immediately. From speed of autocomplete to the ease of seeing what was happening, it felt like a better feedback loop.

In particular, comparing against Copilot, I found the UI and responsiveness to be shockingly faster. I didn't realize how accustomed I'd become to the delay of Copilot.

I used Cursor primarily with Claude 3.5 Sonnet. 

Here's a video of using Cursor to fix the url structure:

<iframe width="560" height="315" src="https://www.youtube.com/embed/Y_V636f5giM?si=4kBtY0LP2n8_IK6Y" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>

As mentioned earlier, the migration would break the URL structure, so I asked Cursor to match production behavior. Initially, it rewrote some other files which linked to the posts, but did not rewrite the post URL itself. A subsequent edit fixed that.

Here's the final URL rewriting logic in `src/pages/[...slug]/index.astro`:

```ts
export async function getStaticPaths() {
  const posts = await getCollection("blog", ({ data }) => !data.draft);

  return posts.map(post => {
    console.log(`Processing post: ${post.slug}`);
    
    const [year, month, day, ...titleParts] = post.slug.split('-');
    const slug = `${titleParts.join('-')}.html`;
    
    console.log(`Generated path: /${year}/${month}/${day}/${slug}`);
    
    return {
      params: { year, month, day, slug },
      props: { post },
    };
  });
}
```

Not terribly complicated, though I appreciated that it handled the pathing for me as well.

Additionally, I mentioend needing to replace post metadata. It did two things I really liked. One: when I asked it to replace metadata, it not only did that for multiple posts, but it applied a pretty thoughtful transformation. 

Here's what I asked:

> Migrate the date field and provide a description for the blog posts

Before:

```
---
layout: post
title: Reflections on my Amazon Career
date: 2022-06-03 07:57:01.000000000 -07:00
---
```

After:
```
---
title: Reflections on my Amazon Career
pubDatetime: 2022-06-03T07:57:01-07:00
description: "After four years at Amazon, I wanted to share what made Amazon successful across so many industries. Here's what I learned about engineering culture, Leadership Principles, and building customer-focused teams."
tags:
  - career
  - amazon
  - leadership
---
```

_and_ it applied this transformation to several posts.

Lastly, Cursor's autocomplete is great and it's easy to see what's happening.
For example, I started editing a post for the color is red post. It had Python shell code in it, and Cursor was able to highlight the code and provide autocomplete for the Python code.

<iframe width="560" height="315" src="https://www.youtube.com/embed/tWZBZLbR_TA?si=4kBtY0LP2n8_IK6Y" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>
In this post, you can see it figuring out that I want to edit it to be more like the Terminal output. It then suggests applying the same change to additional prompts. When I correct it so that the Terminal output is not `>>>` prefixed, it does that too.

Also, it's so fast that you almost cannot tell that it's auto-completing, but I hit tab to accept the changes as we went.

### Conclusion

In the end, I was able to migrate the blog with Cursor in about 3-4 hours, including updating descriptions for 43 posts, fixing the URL structure, and tweaking styling / icons / etc.

Notably, this doesn't include the manual steps I added at the beginning, though I think I could've skipped some of the tutorial steps given how much the tooling helps.

I'm happier with the CSS and styling, and it gets better [Page Speed Insights](https://pagespeed.web.dev/) scores than it did before. 

Here's the final initial result:

<img src="/assets/ai-blog/blog-newhome.png" alt="Final homepage" />
<img src="/assets/ai-blog/blog-newpost.png" alt="Final post" />

Here's a summary of the cost and times:

### Cost Effectiveness

   - Aider/Claude: ~$10 for partial migration attempts
   - Cursor: Basically zero, I used the trial version and was able to do the migration without any additional cost.
   - Manual Migration: Estimated 8-10 hours of work


### Best Practices
   - Start with a working template
   - Use AI tools for repetitive tasks rather than full migration
   - Keep human oversight for important decisions
   - Test thoroughly after automated changes

### Tool Comparison
   - Aider: Better for targeted code changes, struggles with bulk operations
   - Cursor: Excelled at repetitive tasks, provided better context awareness
   - Traditional Methods: More time-consuming but predictable

### Final Thoughts

The migration showed that AI tools can significantly speed up certain aspects of web development, but they're not yet ready to handle complete migrations autonomously. Cursor proved to be the more practical tool for this specific use case, offering better control and faster iterations without the cost overhead of API calls.

For developers considering a similar migration, I'd recommend:
- Starting with a working template
- Using AI tools for specific, repetitive tasks rather than the entire migration
- Maintaining careful version control
- Verifying all AI-generated changes


AI tools like Cursor show tremendous promise for simplifying migrations, but they still require human input for critical decisions. Developers considering similar projects should approach AI as a helpful assistant rather than a complete solution.
