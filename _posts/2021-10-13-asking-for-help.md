---
layout: post
title: Getting Unstuck
date: 2021-10-13 20:00:01.000000000 -07:00
---

One of the most frequent conversations that comes up when I'm working with
other engineers is: how do I ask for help? How do I find what I need to locate
if I don't know where to look? What do I do if I keep getting stuck?

### Try the Obvious

It can be maddening to work through an error that seems like it should
be obvious. Why the heck isn't this thing working? 

First, a brief story. I started my career working in the post production
industry as a Systems Administrator. That meant that my colleagues came to me
when something didn't work as they expected. I got a reputation as
someone frustrating to call upon because I'd solve the problem
and make the other person feel silly for asking for help
(unintentional, I swear!). 

What I've found is we tend to try the advanced solutions and assume
that the problem is a complex one. It can be easy to overlook 
a simple solution. This is part of what can make calling Tech
Support lines so frustrating. Of course I've checked the power and
tried rebooting the computer. 

One example: A colleague mentioned that their hard drive would not
mount. They tried unplugging and replugging it, moving it between
computers, and restarting the machine. They tried different cables. They
checked that it was showing in the disk utility and RAID tools. So what was
it? They hadn't checked whether it was the right drive.  In this case,
clients delivered two hard drives to our facility at roughly the same time.
My colleague grabbed the wrong one by mistake, which I learned by 
looking at the hard-drive and checking its barcode against in our inventory system.

So, when a colleague asks for help or when I get stuck, I start from
first principles and do something like this:

1. **Read and re-read the complete error message.** Is
there something obvious it's saying I should do, hidden in a misleading error
message? For example, we may see that a build failed only to find that it was
due to a failed style check in the code. 
1. **Try the simplest thing that could fix it.** Could it be a network connection
problem? Have I tried restarting the machine? Is the cable connected? What happens
if I back out of my code change or `git stash` it, does it work then?
1. **Do an internal search.** Do we have documentation which covers this
edge case? Is this a known bug? Is another team working to resolve
an outage or service degradation?
1. **Find an implementation reference.** Is there an example on Github
or another project where someone has done what I'm trying to do? What can
I learn from their implementation and how it differs from mine?
1. **Do an external search.** Does Stack Overflow or the like have
information on the error?

If none of those things work, I'll ask for help from a teammate or someone I
suspect may know the answer. 

If these steps sound obvious, that's the point! It's easy to overlook
these obvious-sounding fixes and assume the problem is more challenging than it
is.

### How to Ask for Help

If I'm trying to figure something out, I try the above steps for about 30
minutes. If I'm still stuck, I ask for help, 
which can include asking a specific teammate, a chat channel, or posting to
 Stack Overflow. The format I've found most successful is this:

1. What I'm trying to achieve and what I'm experiencing
1. What research I've consulted so far 
1. What isn't working as I expect 
1. What I've tried so far 
1. A specific request

For example, let's say we're having trouble getting a build to pass its tests. I
might post something like this:

> I'm trying to build the iOS project and it's failing the build with an error
> unrelated to my change.  I followed the internal wiki for setting up my
> developer environment and I've checked out packages X and Y.  As per the
> instructions, I built Y and then X, only for X's build to fail saying that Y
> is missing a dependency.  I've validated that Y has the dependency listed in
> its configuration file.  Could you help me see if I'm doing something wrong
> or if Y is importing the file incorrectly? 

In this example, we start by identifying our goal (build the iOS project) and
what we're seeing (an error unrelated to my change). We go through what has
been tried so far (read wikis, check dependencies) and what's not working
(dependency missing). Lastly, we ask for something specific
from the teammate or person with whom we're discussing (review / file import
check).

This may seem like a lot of work to ask for help! Can't we take a shortcut and
just say, the build isn't passing? Yes, that can be a valid approach,
particularly if the audience is amenable to that. Here's why I prefer this
approach:

1. Structuring my question this way shows that I respect the time of
    whomever I'm asking. I've compiled as much information into the
    initial question as possible. I'm sharing the context of what I've
    looked at and tried. It requires fewer follow-up questions.
1. Preparing my questions allows me to go through a rubberduck
    process where I'm forced to make sure **I** understand
    what I'm asking for help with and that I've done due dilligence on the problem.
1. By making a specific ask, I'm more likely to attract the attention of
    someone who can help than if I were to say "Who knows iOS and can help me with
    a build problem?". Were someone to pose such a general question, it can be
    intimidating to chime in since the person may know iOS and yet not know how to help
    with a specific iOS build problem.

### What to Do If No One Can Help

Even after trying these steps and asking for help, I may not
find someone who knows the answer to what I'm looking for. Then we get to an
interesting fork in the road, where I'll do one of the following:

1. Ask for a referral. Sometimes I can ask someone else for help, or the
person whom I'm asking might be able to refer me to an expert on a particular
topic. 
1. Keep digging. In this case, I'll keep looking into the matter. Sometimes you
are working at the edge of something that no one knows yet and it needs
more time.
1. Re-examine what got me here. In a rare case, I may encounter something
niche when I do something off the beaten path. For me, the most
notable example of this is when I [embedded a Django application in a
self-contained OSX executable](https://stackoverflow.com/a/16180619). I
 may have been the first
person to ever do this. That's not a good sign! If 
you're doing something particularly unusual, it may be best to go back to more
familiar ground and try a different approach.

If you find yourself getting stuck multiple times a day or you're not sure
where to start, it may be
that you don't know the resources available to you. Perhaps there's a search
engine you could use.  It may be worth asking your teammates how they look for
resources and see if they have a different process for searching.


### There's No Shame in Asking For Help

One last point I'd like to make is that asking for help or admitting you don't
know something need not be a source of shame. Calibrating these skills takes
time and practice.  

The most common mistake I've seen is to avoid asking for help out of fear of
judgement.  I've seen engineers try for a day or more to find a solution to
something where a teammate could have helped shorten that time, had they asked.
Even as you gain experience, this doesn't go away.  You'll still get stuck
 and being able to admit that you don't know the answer is a kind of
super power on its own. 

With that, I wish you luck and I hope you find a solution to any challenges you
may encounter.