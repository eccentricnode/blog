---
title: "I Spent a Year Using Zettelkasten Wrong"
date: 2026-01-12
draft: false
tags: ['productivity', 'note-taking', 'zettelkasten', 'knowledge-management']
description: "I spent over a year creating perfect zettelkasten notes. They were atomic, linked, beautifully formatted, and completely useless. Here's the fundamental mistake I made."
---

For over a year, I followed zettelkasten principles religiously. My notes were atomic, containing one idea each. They were linked together with connections everywhere. They were beautifully formatted with clean markdown, headers, and structure. And I created them immediately while learning, exactly as I thought I was supposed to.

My notes looked beautiful. They were technically correct. And they were completely useless.

The result of all that work was hundreds of notes and zero value. Nothing to show for it. I would spend three hours on a thirty-minute course because I was creating "perfect zettelkasten notes" on every concept. By the time I finished, I was exhausted, the notes were pristine, and I never looked at them again.

Eventually I just abandoned most of them. My boot.dev notes are still sitting in my system, hundreds of perfectly formatted notes I never use. My zettelkasten notes about zettelkasten itself met the same fate. Not deleted, just dead weight I step around.

Then I read Bob Doto's "A System for Writing" and realized the fundamental error I had been making for over a year. I had been using a writing method for note-taking.

---

## The Revelation

Here is what nobody tells you about zettelkasten: it is a writing system, not a note-taking system.

Your notes are input. Your zettelkasten is output.

This distinction sounds simple, but missing it destroyed my entire system. Let me break down what I failed to understand.

There are three types of notes, not one. The first type is fleeting notes. These are random thoughts during the day, shower thoughts, conversation insights, passing ideas. They get captured in your inbox and processed weekly. Their lifespan is measured in days. If you do not process them, they rot.

The second type is reference notes, sometimes called literature notes. These are notes taken while consuming material such as books, courses, and videos. They are quick captures of what the source says, not what you think about it. They are not processed yet. They are simply marking what matters, serving as your bookmark back to the original material. You can always come back to these later. Their lifespan is permanent. They form an archive of what you consumed.

This second type is what I was missing entirely.

The third type is zettelkasten notes, your permanent notes. These represent your synthesized thinking built from reference notes. This is where you develop ideas and make connections. They are created in dedicated writing sessions, not during consumption. Their lifespan is permanent and evolving. This is your actual knowledge base.

The workflow, properly understood, moves through distinct phases. First you consume material and create reference notes. This is input. Later, during weekly processing, you think through what you captured. Then you create zettelkasten notes. This is writing, this is output. Finally, you use those zettelkasten notes for content creation, whether blog posts, articles, or whatever you produce.

---

## How the Problem Compounded

This near-dogmatic approach to following zettelkasten caused real problems beyond just wasted time. I stopped taking the writing itself seriously.

Because my system had become a pile of garbage, and I was trying to link new ideas to this mess, I just gave up. I started procrastinating on going through my notes at all. I knew there was nothing of value waiting for me.

The critical mistake was not distinguishing between fleeting notes and reference notes. I never separated my random daily thoughts from the notes I took while reading and consuming material. I saw them as equally valuable. Both went into the same inbox.

This caused cascading issues that fed on themselves.

The first issue was a massive pile of notes with no references. At the end of each day I had an enormous pile of notes with no connection back to original content. I could not remember whether I had thought something myself or read it somewhere. I lost all connection to sources.

The second issue was that I could not distinguish my own thoughts from content I consumed. Daily thoughts mixed with course notes. Book insights mixed with shower thoughts. There was no way to tell what was my idea versus what I had absorbed from elsewhere. Processing became impossible.

The third issue was a vicious cycle. My inbox filled up endlessly. I knew there was nothing of value in there. So I avoided processing it. Which meant it filled up more. Which meant I procrastinated harder. Which meant the system became useless.

My inbox became a graveyard. Hundreds of notes I knew were worthless, so I never processed them, so they stayed worthless.

---

## What I Was Doing Wrong

The exhausting method I followed looked like this. I would start reading course material. Then I would stop. I would create a perfect zettelkasten note, formatting it properly, linking it to other notes, synthesizing it into atomic form. Then I would continue reading. Then I would stop again. I would create another perfect note. More formatting, more links. I would repeat this until exhausted.

The result was perfect notes and unfinished courses. Burnout was inevitable.

Here is what I should have done instead, following what Bob Doto describes in his book. I would read course material and take quick reference notes. Just brief captures like "Chapter three covers how functions are first-class in Go" or "Chapter four explains goroutines versus threads, benchmark shows ten thousand goroutines run without problem." I would keep reading. I would mark more key points. I would finish the course. Consumption complete.

Then later, in a separate writing session, I would review those reference notes. I would ask myself what I actually think about this material. I would write a zettelkasten note representing my own synthesis, something like "Why Go's concurrency model enables different design patterns." I would link it to other zettelkasten notes. I would develop the idea.

The result would be fast consumption, deep synthesis, and usable knowledge.

---

## The Timing Problem

The critical mistake was doing writing work during the capture phase.

When consuming material, you should not create perfect notes. You should not format extensively. You should not synthesize yet. What you should do is capture quick references, mark what seems interesting, and finish the material.

Later, during weekly processing, you review those reference notes. You ask yourself what you think about what you captured. You write zettelkasten notes, which is where synthesis happens. You link them together. This is where you do the actual thinking.

Capture requires low effort. Writing requires high effort. These must not be mixed.

---

## A Concrete Example

Let me show you the difference with a real example from learning Go.

Under my old, wrong approach, while taking the boot.dev Go course I would create a note like this. The title would be something like "Goroutines Enable Cheap Concurrency." I would add tags for Go, concurrency, and performance. Then I would write a full explanation: "Go's goroutines use an m:n threading model where multiple goroutines are multiplexed onto a smaller number of OS threads. This design choice makes goroutines extremely cheap to create compared to traditional OS threads because the goroutine stack starts at two kilobytes versus one to two megabytes for OS threads, context switching happens in userspace, and the Go runtime manages scheduling." I would add links to notes on threading models, the actor model, and concurrency versus parallelism. I would note the source as the boot.dev course, chapter four, section three.

I would spend fifteen minutes on that single note, during the course itself. The result was exhaustion after three chapters and never finishing the course.

Under the correct approach, while taking the course I would create a simple reference note titled "boot.dev Go Course Reference Notes." Under chapter four on concurrency I would jot down bullet points. Goroutines use m:n threading model. Cheap to create, two kilobyte stack versus one to two megabyte threads. Userspace context switching. Benchmark showed ten thousand goroutines running without problem. Section 4.3 has good visual diagram. Key quote: "Goroutines are cheap enough to use liberally."

I would spend two minutes on that. I would keep moving through the course. I would finish the course in two hours with all the key points captured.

Then later, in a dedicated writing session, I would create my zettelkasten note. The title would be "Goroutine Model Enables Different Concurrency Patterns." The content would be my own thinking: "Unlike thread-based concurrency where threads are expensive, Go's goroutines are cheap enough to use liberally. This changes how I approach concurrent design. I do not need worker pools because goroutines are cheap. I can use a goroutine-per-request pattern. This is similar to Erlang's actor model but lighter weight. This matters for my projects because my AI content engine could spawn goroutines for parallel LLM inference calls without resource concerns, and my game project could handle thousands of concurrent player sessions easily." I would link to my notes on event-driven architecture, the worker pool pattern, and the Erlang actor model. I would reference back to my boot.dev reference notes.

I would spend twenty minutes of deep thinking and synthesis. The result would be my own insight, connected to my own work, actually useful.

---

## Why Nobody Caught This

The zettelkasten community has a visibility problem. People do not share their actual zettelkasten because it is extremely personal.

What you see in tutorials and blog posts is explanations of why zettelkasten works, tutorials on how to format notes, and discussions of tools and workflows. What you do not see is the messy reference notes phase, the weekly processing ritual in action, the distinction between input and output, or the actual timing of when different notes are created.

The result is that you copy the output, those perfect zettelkasten notes, without understanding the input, the reference notes, and the process, those weekly writing sessions.

It is like seeing a finished essay and thinking you should write like that on your first draft.

---

## The Four Systems Running in Background

Once I understood the distinction, I reorganized everything into four layers that run continuously in the background.

The first layer is daily capture, fleeting notes. The purpose is catching fleeting thoughts. The format is quick and messy with no formatting required. These live in an inbox folder. They get processed in weekly review.

The second layer is the reference archive, literature notes. The purpose is capturing what sources say. The format is bullet points, key quotes, page numbers. These live in an input folder organized by type, whether books, videos, or courses. They form a permanent archive. You can always come back to these.

The third layer is the knowledge base, permanent notes. The purpose is your synthesized thinking. The format is developed ideas linked together. These live in your zettelkasten folder. They are built from reference notes during review sessions.

The fourth layer is the sleep folder, future ideas. The purpose is holding ideas that are interesting but not useful right now. The format is raw ideas and future possibilities. These get reviewed periodically. This prevents losing good ideas that do not fit current projects.

The system runs continuously. Fleeting notes flow into the inbox and get processed weekly. Reference notes flow into the input folder as a permanent archive. Review sessions pull from references into the zettelkasten. The sleep folder catches ideas that are not ready yet. And everything eventually feeds into projects and content creation.

---

## The Sleep Folder

Bob Doto mentions a sleep folder in his book, and this concept is brilliant. It is a place for ideas that are interesting but not immediately useful, future possibilities, ideas that need time to develop, things that do not fit current projects.

This prevents several problems. You do not lose good ideas just because they are not relevant right now. You do not force ideas into your zettelkasten when they do not fit yet. You do not process too early, because some ideas need time to mature.

The workflow during a review session has three possible outcomes for each reference note. If the idea is clear and useful now, it becomes a permanent note. If the idea is interesting but not ready, it goes to the sleep folder. If the idea is not useful, it gets deleted.

Not everything needs to be processed immediately. Some ideas need context you do not have yet. Future projects might make sleeping ideas relevant. Reference notes can sit for weeks or months. You can always come back to them. Trust the process.

---

## What Changed

Before understanding this distinction, my system was useless. I had hundreds of perfect notes with nothing to show for it. Taking courses was exhausting. I never finished material. I eventually abandoned most of my notes. I could not create content from them.

After understanding the distinction, consumption became fast because I just mark key points. Reference notes are messy, and that is fine. Weekly processing is where I think deeply. Zettelkasten notes are my actual insights. Content creation pulls from the zettelkasten easily.

---

## How to Fix Your System

If you are struggling with perfect but useless notes, here is how to fix it.

First, separate reference notes from your zettelkasten. Create an input folder for reference notes. Keep your zettelkasten folder for your synthesized thinking. Stop trying to create perfect notes while consuming material.

Second, change your capture workflow. When reading material, take quick reference notes in your input folder. Just bullet points, key quotes, page numbers. Do not format. Do not link. Do not synthesize yet. The goal is to finish the material.

Third, add a weekly writing session. Review your reference notes from the week. Ask yourself what you think about what you captured. Write zettelkasten notes, which is where synthesis happens. Link your zettelkasten notes together. This is where you do deep thinking.

Fourth, create content from your zettelkasten. Your zettelkasten notes are your ideas. Turn them into blog posts, articles, threads, whatever you produce. Reference back to sources when needed.

---

## The Key Insight

Zettelkasten is not a filing system for information. It is a writing workshop for developing ideas.

Your reference notes are ingredients. Your zettelkasten is the cooking process. Your content is the meal you serve.

Do not eat raw ingredients. Cook with them first.

---

## Why This Took a Year to Discover

Most zettelkasten teaching focuses on how to format notes, making them atomic and linked. It explains why zettelkasten works, emphasizing connection over collection. It discusses tools and workflows like Obsidian and Roam.

Almost nobody talks about the difference between reference notes and zettelkasten notes, when to create each type of note, the weekly processing ritual, or the two-phase workflow separating capture from writing.

Nobody shares their messy reference notes. You only see the polished zettelkasten output and assume that is what you should create while consuming material.

---

## The Practical Difference

Consider consuming a two-hour course.

Under the old, exhausting approach, two hours of video became six hours of note-taking. I would produce forty perfect zettelkasten notes that I never looked at again. I would not finish the next course because I was burned out.

Under the new, sustainable approach, two hours of video requires twenty minutes of reference notes, just quick captures. I finish the course. A one-hour weekly writing session produces five to eight zettelkasten notes representing deep synthesis. Those notes feed a blog post and other content.

Time saved: five hours. Quality: higher. Burnout: eliminated.

---

## If You Are Just Starting

Do not make my mistake. Start with the full system from the beginning.

Create three folders. An inbox for fleeting thoughts captured daily. An input folder for reference notes taken while consuming material. A zettelkasten folder for your synthesized thinking, your writing.

Understand the timing. The capture phase should be fast, messy, and low effort. The writing phase should be slow, thoughtful, and high effort. Do not mix them.

Set up weekly processing. Pick a day, perhaps Saturday or Sunday. Review your fleeting notes and reference notes. Write zettelkasten notes through synthesis. This is where the value is created.

Remember the core distinction. Reference notes are input, capturing what sources say. Zettelkasten is output, capturing what you think. They are separate layers in the system.

---

## In Summary

I spent a year creating perfect, useless notes because I was using a writing system for note-taking.

Zettelkasten is not how you take notes. It is where you write from your notes.

Reference notes are fast and messy. They are input. Zettelkasten notes are slow and thoughtful. They are writing. Content creation pulls from the zettelkasten. It is output.

Three separate phases. Three separate purposes. Do not mix them.

Now if you will excuse me, I have a year's worth of reference notes to properly process into my zettelkasten.

---

## References

Bob Doto, [A System for Writing: How an Unconventional Approach to Note-Making Can Help You Capture Ideas, Think Wildly, and Write Constantly](https://www.amazon.com/System-Writing-Unconventional-Note-Making-Zettelkasten/dp/B0D7GX2J9L)

Sönke Ahrens, [How to Take Smart Notes: One Simple Technique to Boost Writing, Learning and Thinking](https://www.amazon.com/How-Take-Smart-Notes-Technique/dp/3982438802)

Niklas Luhmann, the original zettelkasten method
