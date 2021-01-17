---
layout: post
title: "How to make a writeup"
date: 2021-01-17
---


Sharing writeups are a common staple of post CTF ritual. They're great for:

1. Showing your thought methodology and by an extension,  logical thinking process
2. if you've won a prize, they're a great way to validate your completion of challenges
3. Learning new categories,  and types of challenges, and using this to overall improve your CTF skills
4. and for organisers - learn about alternate solutions for your challenges,  and maybe use these ideas to make new challenges.

I am by no means a guru in making writeups,  I just read a lot,  and make some on occasion. This also isn't a guide on how to do lots of different types of challenges, although I will throw in examples from time to time. Hopefully by doing this, you'll improve your writeup skills, and transfer these to other aspects of your life, like essay writing.

---

## Tip 1 - Be concise, but thorough.

At first, this may seem like an oxymoron, but you shouldn't waste more time than is needed. However, you should be thorough with everything you do, and don't skip over an important step; remember writeups are a really good resource to look back on for not only other teams, but you and your teammates, to learn and consolidate skills. For example, have a look at the source for this simple pwn challenge I've made:

```c
#include <stdio.h>
#include <string.h>

int main(void)
{
    char buff[15];
    int limit = 0;

    printf("\n Enter the password : \n");
    gets(buff);

    if(strcmp(buff, "thejamsecbloggg"))
    {
        printf ("\n pwn me better \n");
    }
    else
    {
        printf ("\n you pwned me nya! \n");
        limit = 1;
    }
    if(limit)
    {
        printf ("\n Take the flag nya! \n NjYgNmMgNjEgNjcgN2IgNzAgNzcgNmUgNjUgNjQgNWYgNmQgNjUgNWYgNzUgNzcgNzUgNWYgN2Q= \n");
    }
    return 0;
}
```

(if you can be bothered, compile it with `gcc source.c -o vulnerable`

A bad writeup would be something like the following:

spam the program and decode the text for the flag.

Why is this bad?  

- Doesn't explain why you did what you did
- Very vague
- No flag at the end

A better example of a writeup would be:

After looking at the source code, we can see that the program is vulnerable to a simple buffer overflow, which if what we enter is over 15 characters, it will add 1 to the variable `limit` , printing a secondary string to the user. We can use the printf command, and pipeing it's output into the program to achieve this. The resulting output in the terminal was:

```bash
➜  Downloads printf 'rfn4uifu4bufigb43uibuib4iub\n' | ./vulnerable

 Enter the password :

 pwn me better

 Take the flag nya!
 NjYgNmMgNjEgNjcgN2IgNzAgNzcgNmUgNjUgNjQgNWYgNmQgNjUgNWYgNzUgNzcgNzUgNWYgN2Q=
```

The equals sign at the end of this string may signal to it being base 64 encoded, we can use a tool called [cyberchef](https://gchq.github.io/CyberChef/) to decode this.  After using magic on the string in cyberchef, we see the string is encoded in base 64, then hexadecimal. After decoding both of these, we get the flag of: `flag{pwned_me_uwu_}`

Why is this better?

- Explains with detail what was done, but didn't overcomplicate anything
- Relatively consise
- Gives a flag at the end

---

## Tip 2 - Format

If you are making a lot of writeups for a CTF, you'll want them to follow a format, to keep things easier to understand for the reader to jump between writeups, a bit for ease of reading. Assuming you're using [gitbook](https://www.gitbook.com/), (and if you aren't you really should be), make a page group for the CTF, then if you've done around 1 or 2 challenges from each category, make a page for the category, then make a sub page for each challenge. For ease of copy pasting, use this format:

```markdown
# [Challenge Name]

### [Category(if not specified in main page title)]

### [Points]

[Description]

[How you did the challenge here]

[Solve script? (if any)]

#### [Flag here]

[misc notes here, e.g alternative solutions, possibly even a summary of what you learnt for harder challenges]
```

---

## Tip 3 - Writing for your audience

This should be a quick one, but your audience will mainly be technical people, who know their way around a command line with basic commands; you don't need to explain to people the full process of listing files in a directory, or installing a python module. However, this doesn't give you an excuse to slack on all parts of your writeup; also don't assume that people know how to solve a challenge, just because you can.

---

## General Ettiquette

Here's some general rules/ tips to abide by, when making writeups, not all of these will be said explicitly, so use your judgement.

- Firstly, don't publish writeups for CTFs that are still active/ HTB boxes or challenges that aren't retired; these ruin the experience for everyone.
- Use a popular website to share your writeups, i.e a Github repo or gitbook.
- It's always a nice little touch to give CTF organisers a little shoutout.
- Consider providing challenge files, it's always a nice touch

---

## Final Thoughts

Firstly, why wasn't this as long as other posts? Well, I didn't *really* have too much to say, so as tip 1 said, there's no point in elongating something that doesn't need to be stretched out.

Anyways, I hope you've gained something by reading my first cybersec/ CTF related blog! Hopefully there's more to come 😃

---

Blog post by Jammy

17/01/2021
