+++
title = 'Lccp Filter Self Made Tools'
date = 2026-03-26T13:10:12Z
draft = false
description = "Building a schema-led LCCP filter and gap analysis tool using AI — from compliance frustration to a self-hosted, Docker-deployed prototype."
tags = ["LCCP", "Filter", "Tools", "AI"]
+++

My first steps on this journey were when I started experimenting with AI to help me build prototypes. Initially, this was giving me detailed instructions and code to copy and paste; .html prototypes worked immediately in my browser and I could iterate again and again. This isn't the first tool or project. This is the second one that was almost an afterthought? The add-on?

In work, one of the main frustrations for me and some of my peers is that one of the regulations, the Licence Conditions and Codes of Practice (LCCP), is quite long at around 116 regulations spread over multiple licence types, and there's no filter. There are several extracts, but when I was first shown these it was pointed out they are not 100% accurate in limiting the regulations to only one type of licence.

I have copied the LCCP into Excel (and other flavoured) sheets at multiple points throughout my career, line by line at first, or in chunks with formatting editing. Over the last year, there have been many times when having the ability to filter by type of licence or regulation would have been pretty useful. Whilst there is a search function in the electronic version currently, myself and many people I know prefer to work from the print version which shows the complete regs at the same time.

I attempted a few times to make my own filters in spreadsheets, but the issue is some of them state they apply to named licences like Casino, some of them say they apply to all remote licences, and some of them state everyone apart from these two licences. This means, regardless of anything else, making these into a usable filter would need the addition of a number of columns to identify when a reg is relevant. I think I got 10 regs into this before realising it was a terrible idea and calling it a day.

However, when I started coworking with AI, the first project I made extracted information from the AML guidance and organised it by licence, in order to make an AML Risk assessment tool. My thoughts when I had a working prototype of that were: yes, this is great, you have a risk assessment for just your licence(s). However, when you are writing your AML policy, you need to know the regs which are also applicable. This led to an LCCP filter and Gap analysis tool.

My attempts at making a filter using Excel had given me an idea of the blockers of that route. However, the solution to that, in many ways, was how this was going to be built. If I had a schema which extracted everything I needed from the regulations, and when each regulation was extracted it had the additional bits and tags added, it would be a future-update-proofed solution and the data could be reused for as many projects as I needed.

A schema was made and reviewed, and then AI was used to batch extract the regulations from a text document, with QA and checks built in. The finished version was great. The actual filtering using that is incredibly simple to build, and it ended up having a gap analysis tool built into it so you can log which regs you have mapped to a policy, procedure, or other control, and you could then print this out to map your gaps.

This was left behind as I moved into other new and interesting prototypes and ways of learning, until this year. I made myself a homelab to help educate myself. Self-hosting programs using containers and some of my self-made tools brought me to the realisation that maybe cloud would combine these skills and experiences?

I started working through AI-written run books, launching instances, installing Docker, having it deploy Nginx... and it looked familiar? It was just like when I made those first tools and prototypes? npm build and npm run. Making them work locally, then as a container on my home server, then eventually just deployed from my GitHub using Portainer's ability to deploy automatically like that. I know I learn from doing, and I know that having something relevant and real makes it worth it for me. So, I extracted the filter from the subfolder of that original project's repo, gave it a polish, and made a fresh repo for it. Since then, the AWS reps that teach me to deploy with Docker are using my own tool that I made.

It's not the first tool I made, it's not the first tool I self-hosted, and it's not the first tool I deployed from GitHub to my home server or to a free domain via Cloudflare. However, it's what I cloned and made into an image and pushed and pulled. It's the first that I ran on AWS. It's the first I saw on my domain (where this blog lives).

It's simple, and it took 22 seconds to build in AWS the first time. (The run book suggested I might want to go make a brew as it might take a while at that stage!) However, when I bootstrapped my first instance instead of SSHing in, this is what I saw as proof on my phone. This is what I first had on a self-healing fleet. Having something that was mine, that I know is useful, but that I could and can edit to fit the requirements, makes it special to me.

I like that my simple testing tool was also my first schema-led design, and that I have carried it with me. It makes me feel like a blacksmith whose first task as an apprentice is making their own hammer and tongs. I could make it more complicated, add more features, or advertise that it exists to people who might actually use it. But it doesn't need that because it's taught me the importance of a schema and lightweight, simple design. The lessons through its creation and life can be applied to many other regulations and sources of data. It's definitely better than the "write your own calculator/calendar" starter projects that were in my original ideas list, because it might be original as well.