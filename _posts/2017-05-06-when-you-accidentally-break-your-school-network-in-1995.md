---
layout: post
title: When You Accidentally Break Your School Network in 1995
published: true
twitter_plug: true
---

In my last post, I reminisced about [my bbs software that I wrote and sold in 1993](/2017/04/18/my-bbs-software-from-1993/). In 1995, I 
was a senior in high school, and my school had just purchased a 76 computer Novell network for the 900 students to use. Nobody in the 
school's staff had a background in maintaining computers or a network, but this was a state of the art system that they had bought, 
so surely it would keep purring without a hiccup. Right? 

<!--excerpt-->

<em>
	Update: This post was front-paged on Hacker News, and you can [see the discussion here.](https://news.ycombinator.com/item?id=14280000)
	Thanks for the conversation HN!
</em>

### No policy meant running programs from home

There was no policy around the usage of the computers, and bringing in files and software from home on a floppy disk was typical. Having access 
to computers during the day was a dream for me. I didn't have to wait to get home from school to play with computers, and there was even an 
AP programming class.

### The night before that fateful day

I had found an interesting piece of software on a bulletin board system called KKV. It was a key capture utility with no documentation, and
I remember it was version 0.90. It was called KKV 0.90. Key Kapture Version 0.90. I obviously knew that this *could* be used to capture 
passwords, but I was curious if it worked at all. Could it really capture all input made from the keyboard, across all programs that the 
input was made to? I had never come across a utility like this. I couldn't imagine how to write a utility like that myself and if it worked, 
it was impressive that someone else had.

I scanned it for viruses with McAffee Antivirus, as I did with anything I'd download, and it came out clean. So, I copied KKV 0.90 to a disk 
and put it in my bookbag to bring to school.

Why didn't I try it that night on my own computer? Good question. Maybe I wanted to show off and run it in front of 
someone else. Maybe some part of me was scared to try it alone. Maybe I was nervous about running it on my own computer.

This was a time before Google.  There were no search engines to return the results of other people's experiences with this software. I was
going to try it at school the next day and find out how it worked.

### That fateful day

As most hackers do, I began my day by telling my mother about my plan.

I told her how I had found this interesting key capture utility, how it could be used to capture passwords, and how I wasn't going to use it 
for that. I explained how I was going to try it out at school that day, on myself.

She didn't seem to think that sounded like a good idea. But whatever, Mom.

### Running the program

At the end of the school day, with a friend standing behind me in the school library, I ran the KKV program from DOS. 

I then typed commands in DOS. I launched some programs and typed in them. Everything that I typed was, in fact, saved to a hidden text 
file named KKV.90. 

Amazing. It worked.

So, I saw that it worked and it was time to remove it. I deleted the executable KKV program that I had run, and rebooted the computer so 
that it would no longer be resident in memory.

That was that. I was done with KKV. Or so I thought. 

### Something was wrong

A few days later I received a phone call from a friend at school who had mentioned that many of the computers had started to lock up. 
He was a computer-enthusiast that was also in my AP programming class; he was asked by staff to research the problem, so he did. I 
was home sick from school that day.

I was pretty confident that he'd find the problem and fix it. He was a clever guy.

### Discovering the cause

My friend called me again to inform me of a similarity that he had found among the computers that were locking up: they all contained 
a text file called KKV.90. My heart sank.

I explained to him that the utility program that I had run a few days previous logged key strokes to a file with that name.

It didn't take long before all of the computers were locking up in the same way.

I only ran that program on one computer in the library, though, and then I erased it and rebooted the computer! Why was this file on
all of the computers!?

### Trying to fix it

No big deal, I thought. I knew the root cause of the problem, that was half of the battle. Now I just had to fix it.

I considered whether or not I should tell the school's staff everything that I knew. Specifically, that I had run the offending program.
There were rumors of expelling a student if they were found to have caused this, so I thought it was best to just fix it and stay quiet. 
I told my parents everything, and their advice aligned with my own plans. Just fix it.

McAffee was a leading Antivirus software at this time, but it did not detect any problems when ran on the computers that were locking up, so
it was not able to fix the problem.

After some digging I had found something. For every executable (.exe) file on the computer, there was also a shadow 
.com file on the computer with the same filename but a .com extension. These .com files were hidden, and they were very
small in size. If there was a program.exe, there was also a small, hidden program.com counterpart.

If I ran program.com it did the same thing as program.exe, so it was clear that it was launching the executable, likely after doing 
something else (like loading the memory resident KKV behavior).

I also learned that when running "program" with no extension (as most people do), and there was both a program.exe and a program.com, 
that the operating system gave priority to choosing to run the .com file. When I originally ran the KKV program, rebooted and deleted it, 
it seemed that it was able to live on by making replicants of itself that were ran by running existing programs without specifying a 
".exe" file extension. 

It occured to me that KKV0.90 probably did not stand for Key Kapture Version 0.90. It stood for Key Kapture Virus 0.90. I assumed that
the behavior of locking up the computers was unintentional and a bug in the virus software. 

Removing the virus from a computer boiled down to finding and removing the shadow .com files, but this had to be done on each of 
the 76 computers. I tried different anti-virus softwares and eventually found one that identified the virus and removed the .com files; 
this sped up the process of removing the virus from a computer. I can't remember the name of the anti-virus software that found what 
McAffee didn't, but I remember it was written in another country. Norway?

Having identified the cause as a known virus, and the fix as this particular anti-virus software that was able to identify and remove
it, I communicated this to the school. I offered to come to school over the weekend with my father, who maintained a network at
a college, and fix the problem. The two of us would run the anti-virus software on each of the computers.

However, it turned out that cleaning an individual computer on the network was not enough. On boot, each individual computer on the network
ran a "logon" command that existed on a file server. The file server was infected and so running the "logon" kept reinfecting each of the 
cleaned computers that accessed it. The file server needed to be cleaned first, and then each of the computers that accessed it needed to be 
cleaned. Unfortunately, we were not trusted to use the file server; we did not have the permission that we needed to fix the problem.

The computers continued to lock up and I couldn't do anything about it.

### The hunt

Once it was known that a virus was the cause, the hunt to find the person who did this was on.

Anyone who knew anything about computers was brought into the principal's office and questioned.

A few friends knew that I was the person that the school was trying to find, because I had told them.

One tech savvy friend was called in for questioning and told that he was going to be blamed for everything and that they had
enough information to prove it was him even if it wasn't. He was going to be expelled unless he had any information that he could 
share to prove otherwise.

He was understandably shook and gave up my name. 

### The capture

I was in my AP English class when I was called to the principal's office. I had never been to the principal's 
office before or in any kind of trouble.

I passed my friend in the hallway. He was visibly shaken but I was relieved when he uttered the words "They know."

When administration told me that they knew it was me, I immediately confirmed that it was, and said that I was relieved. I had spent 
so much time thinking about whether or not to come forward, but was scared to. Now the decision had been made for me. I hoped that we 
could get past this. I explained how I had never meant to break anything and wanted to fix the problem. 

The response was that there would be a very visible and severe punishment to come. 

At this point I felt like I had nothing to lose, and amidst the tension in the room, I managed to speak exactly what was on my 
mind. I was not typically this frank with "authority", but in that moment, I'm glad that I was.

What I said was something like this:

"The school's network is like a pool in someone's backyard without a fence or a lock on the gate. There is no policy that said I 
wasn't allowed to bring in software from home, and no anti-virus software to block viruses. If a child walks into the backyard and 
drowns, it is the homeowner's responsibiity. Your network is that home."

Words cannot express the reaction to this statement. I remember it as a lot of huffing, puffing, fist pounding, yelling, and anger.
These words were exclaimed from one staff-member-turned-interrogator to the other,

"MY PILLS. OH MY GOD. GET ME MY PILLS!!"

### Legal action

Charges were brought against FIVE STUDENTS, including me. The other four had absolutely NOTHING to do with what happened. The student 
who watched me run the program in the library was not even one of the five students. They just picked the four most tech-savvy 
students in the school in addition to me.

I believe the charges were for computer theft, a serious charge under a law that is open to broad interpretation. They were seeking payment 
for the cost of hiring consultants to reformat and reinstall software to every computer and the file server in the school. They also 
wanted a hearing with the board of education to talk about being expelled.

There was a stretch of time where I'd go to school expecting to be dragged out in handcuffs. I always thought that would be a very
"visible" punishment like I was told I'd receive.

### Press

I was contacted by the local newspaper and gave an interview. The article was published on the front page. The view of it was that
the school had gotten "caught with their pants down" and hadn't taken the necessary precautions to protect their computers. 

After the article was published, the school offered that if I would stop talking to the press, then they would not expel me. I took 
that deal.

I was able to use [newspapers.com](http://www.newspapers.com) to locate the article. 

<img src="/assets/posts/2017-05-06-when-you-accidentally-break-your-school-network-in-1995/a1-partial-Asbury_Park_Press_Sat__Feb_11__1995.jpg">

<img src="/assets/posts/2017-05-06-when-you-accidentally-break-your-school-network-in-1995/a6-partial-Asbury_Park_Press_Sat__Feb_11__1995.jpg ">


# The outcome

Many students in the school wore white ribbons as a campaign to support the five students.

There were some very supportive teachers who were privately vocal to me about how they didn't support what the administration was 
doing and encouraged me to hang in there.

Some students were just happy to have due dates postponed for homework assignments and thanked me for that.

After many agonizing months (and really, they were agonizing) the charges were dropped and nothing became of them.

One other student and myself then sued the school back for punitive damages and the legal fees incurred. This was not something that I 
was interested in pursuing by the time I was in college, but my mother was. The charges against the school were eventually dropped as well. 

Is there a lesson in all of this? Probably, but I've written enough. 

Be careful out there.
