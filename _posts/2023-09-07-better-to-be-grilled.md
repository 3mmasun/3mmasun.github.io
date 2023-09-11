---
layout: post
title: "Better to Be Grilled?"
date: 2023-09-07 16:00:00 +0800
image: "/assets/img/mount-yari.jpg"
tags: production
---
# A Conversion to Begin With
In a "Release Meeting", where the Devs, the Product Owner (PO), the Business Analyst (BA) and the Senior Manager of Operations and Support (OPS) are all present, a familiar conversation unfolds: 

OPS: "Why are we enabling XYZ feature?" 

DEV: "(Confidently) It's a recommended practice."

OPS: "How are you using them?"

DEV: "Well, in the unlikely event of ABC, we shall have evidents and tools to debug."

OPS: "(Debug in PRD?) Do you have a usecase?"

DEV: "We don't know yet since it's a preventive action."

OPS: "Are there any impacts to other services? What if it crashes another server? (insert 10 more what-ifs)" 

DEV: ... thinking

PO: ... thinking

BA: ... thinking

OPS: "(Facing the devs) Production and staging load are vastly different!"

DEV: "(Why am I the one being grilled?) It's not that serious. Moreover, it's a recommended practice." 

... (replay the conversation for the next 45 mins)

BA: "Alright, the concerns are valid. Let's create a story to track it."

# Our Intention Shapes Our Communication

I'm sure we have all been in such a meeting, whether you are a BA, or DEV, or PM; and to many of us, this is not our favourite kind of meeting.

In this case, everyone, especially the developers, simply recommended and delivered something benefitial in an undesirable situation. But they are now bombarded with questions and concerns that perhaps they have not considered before hand. 

You might feel confused or even annoyed when every WHY, WHAT, WHO, WHEN and HOW are scrutinised. The feature that you are trying release seems to have hit a road block at the very end of the path. And that's totally understable. 

On the other hand, when we are too preoccupied with our own motives, we can lose the oppotunity to identify potential production issues, or even become a little defensive. 

Being able to deliver features fast brings significant advantages to the business, but as the organization's IT systems grow in scale and complexity, the number of unexpected failure points grows even faster. It requires a lot of knowledgeable people to collaborate and think hard about the question: "what else can go wrong, what else?", afterwards, develop a coordinated release plan to minimize undesired impacts.

Whoever pushes code into production, should be eager to find out what are the concerns we have not considered. Those questions are not a reflection of our ability or inability. To enbrace such situation is in fact a sign of our commitment to exellence. 

# A Good Enough Plan

Many years ago I was given the oppotunity to develop a plan to cutover a critical system. At that time, I was just a system analyst in the organization. Although I know the target systems well, everything else is a blank page to me. I know their existence but that's about it. 

While the main sequence of the cutover had been planned out, it was planned to minimize the impact on target systems.

It was only when the plan was shared other senior staffs, that I realized so many things I was not aware of: 
- the infra team has an alert which they shall update and monitor the new the linkage instead
- another team is expecting an output from a cronjob running at the time I planned to switch the linkage
- I have not realized that SFTP server is syncing the files to old and new folders which could result in duplicate transactions
- just to name a few ...

It seems like, each time someone came to the meeting, they would always bring up something new! 

As you have probably figured, many rounds of review and finetuning followed, more checkpoints placed in the process. And most importantly, the plan had evolved to be revertable, with tradeoffs. Nevertheless, it was a great testimony of the collaborative efforts from the people who have contributed to the cutover strategy. 

# Change Our Mindset

While we cannot avoid such meetings from time to time, we can change the way we handle such situations and as result benefit from them: 
- be compassionate
- be open to the possibility that we could be wrong
- look at it as an oppotunity to grow knowledge
- be grateful that some one actually cares and thinks hard on your behalf
- learn from their perpective
- make your plan a little better
- a chance to build a relationship with mutual respect and understanding

With all these, I hope all of us will have a smoother path to production and be proud of what we build. 

