+++
title = "Did the Supply Chain Attack Compromise Me? A Morning Panic Check"
date = 2026-03-31
description = "Walking through my checks for the Anios/plain-crypto-js supply chain vulnerability across my local projects and Docker containers."
tags = ["security", "npm", "docker", "supply-chain", "AI"]
draft = false
+++

It's March 31st 2026, and first I saw a instagram video from Kim the developer talking about how you should get out of bed to check if a supply chain attack affects you, or you might not have a company left in the morning. The last time I saw this happen it didn't seem to affect me, so I assumed this one might not either, but I turned the sound on and listened, and maybe it did? Then I looked on LinkedIn because this is the morning and the time for looking at Instagram and LinkedIn, and people were posting about it, what it does, and how it affects you.

Last night I was using Claude Code to fix some bugs in a tool I made with AI. I had checked if I could host it locally on my Ubuntu VM's Docker stack because Portainer's got some lovely and simple deploy from GitHub functionality, but the build was failing. The process included cloning and building locally, checking errors, fixing errors, pushing changes, repeating over and over until some stability, and then making a pull request and reading what Gemini's opinion of it was. However, tl;dr, there was definitely some upgrading, installing, and npm building going on on my side and on Claude Code locally on my machine's side. 

So obviously I used up my entire usage already this morning on Claude by the time I became aware of this, mostly by being lazy and continuing a conversation. So, Gemini Pro to the rescue! I double-check that this could have affected me, how it could have, and ways I could check. 

YES THERE'S A CRITICAL RISK!!!! potentially... So what's the plan?  

1. **Check your Lock files:** Searching for `package-lock.json`, `yarn.lock`, or `pnpm-lock.yaml`. 
2. **Check your directories for a `plain-crypto-js` directory:** Yes, it normally self-deletes, but the folder sometimes doesn't. 
3. **Rotate exposed secrets:** I didn't expose any secrets, but changing them with my minimal setup isn't too tricky, as I only have 2 or 3 in total that could be compromised. 
4. **Downgrade and pin:** Update your dependencies to forcefully pin the safe versions of Anios until npm flushes the bad releases downstream.

Ok, but like... how? 

```bash
cd <Project directory>

grep -E "plain-crypto-js|1\.14\.1|0\.30\.4" package-lock.json yarn.lock pnpm-lock.yaml 2>/dev/null
```

Nothing showing? Ok, that's good.

How else could I check?
VS Code: open the folder for the project, open the search panel, change "files to include" to `*lock*` and then search for `plain-crypto-js`, `1.14.1`, or `0.30.4`. If you are like me, you then search all files, and then test to make sure the search is working and search for shorter versions of everything—oh, and also `axios`.

What if it's in the Docker images?

```bash
docker run --rm -it job-radar-image npm ls axios
docker run --rm -it job-radar-image npm ls plain-crypto-js
```

So nothing comes up, but... what about dependencies?
Well, the lock files map out the entire dependency tree, and if a package did require it, then the package manager would have written it into the lock file with the version number.

But... What if one of the many rounds of changes added this and then removed it when it didn't work? What if this was done by Claude Code without sharing it, or if an agent did it? The term for this is a 'transient infection', and Gemini gave me a "well done" for asking about it.

How can we check? Well, we can check for dangling Docker images.

```bash
docker images -a

docker run --rm -it <IMAGE_ID> npm ls axios
```

Also, to double-check what I did?

```bash
history | grep npm
```

This means I can review my terminal commands.
Also also, the process was: review, test, fix, review, check, build, check, commit—so the git history can also be checked.

The `docker images -a` search resulted in a bunch of untagged images, and 3 of them matched the size of my backend image, so quick check for them. Nothing came up—big sigh of relief—then, because it's free and there were 7 total, I checked everything.

So no news is good news, and the chance of anything being compromised is low anyways. But running through the checks and then considering the edge cases led to a lovely idea for a ~~Postmortem~~ article.


