---
date: 2019-02-01
title: "Week 26: Finished our preview site"
author: Ian Drysdale
---
**Protecting liberty by simplifying security**

_Recap_: We’re building Fluidkeys to help teams safeguard their source code and protect sensitive data.

## The short version

* We finished making a preview site and announced it on Hacknernews 📣
* We've decided how Fluidkeys will keep a teams keys in sync 🔄
* We've started making it possible to send secret files 📁

## We've finished our preview site of the upcoming release

Last week I shared an early release of our [preview site](/fluidkeys-v1-preview).
It's an attempt to succinctly explain what version 1 of Fluidkeys will do.

This week we critiqued it together and then honed the content. I'm proud of where we've got to.
Then we [announced it on Hackernews](https://news.ycombinator.com/item?id=19044043).
Sadly, no one was interested this time! On reflection perhaps it's better when we actually have
something working to show when posting there. Still, it was good to get the preview site out there
and we've been showing the site to prospective customers. All the feedback has been _very_ positive.
People get our more focused proposition!

It's strange though, what we thought would be a day or so of work actually ended up taking the
majority of the week. This means we've made less progress on the actual application itself,
sadly. Oh well, it goes like that sometimes.

## We've spiked on how team management will work

Paul's been thinking about how the team management and synchronisation will work. To get a
better feel for it, he had a go at making Fluidkeys keep our team's keys in sync with each other.

We've settled on the idea that it'll create a team roster, a list of email addresses linked
to fingerprints and it'll be cryptographically signed by the admin. It'll look a bit like this:

```
uuid = "38be2a70-23d8-11e9-bafd-7f97f2e239a3"
name = "Fluidkeys CIC"

[people]
  [people."paul@fluidkeys.com"]
  fingerprint = "B79F 0840 DEF1 2EBB A72F  F72D 7327 A44C 2157 A758"

  [people."ian@fluidkeys.com"]
  fingerprint = "E63A F0E7 4EB5 DE3F B72D  C981 C991 7093 18EC BDE7"
```

Anyway, he got it working for our team of two! It read the file and refreshed our keys...
Concept proven!

We've written a bit more about how we see it working over [on the preview page](/features/manage-your-team-pgp-keys/).

## Next week you'll be able to send and receive files

Right now, if you want to send another person a secret from the command line you have to either
type or copy and paste it into a prompt. We know people want to send files (certificates, token,
configurations...) so we started on that this week too. We've got sending working. Next week
we'll wire in receiving then you'll be good to go!

That's it for now. Keep warm this weekend, see you next week!

— Ian

*All* feedback is welcome, pop us an email to
[hello@fluidkeys.com](mailto:hello@fluidkeys.com)
