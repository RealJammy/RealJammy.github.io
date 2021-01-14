---
layout: post
title: "Development of The Jambot"
date: 2021-01-14
---

The Jambot is an ever evolving story of personal growth, learning and understanding how people think.

Phrasing the bot like this, it sounds like something incredibly complicated, but at its heart, the concept is very simple - create a simple discord bot that can be used in day to day admining, and other fun stuff. I thought this would be a simple thing that took a couple hours one night, however this ended up being vastly different.

Before I start, this won't be a tutorial on how to make a discord bot - there's plenty of tutorials who can explain it much better than I ever could, instead a story about the challenges and opportunities that building the bot brought up.

One more thing I have to say, a massive thank you to anyone who's helped me with the making of The Jambot, a list will be found below:

- [willwam845](https://github.com/willwam845)

- [potato-jackson](https://github.com/potato-jackson)

- [squishieishi](https://github.com/squishieishi)

- [Day91](https://github.com/Day91)

- [Mystrite]((https://github.com/Mystrite))

- [speccy](https://specatron111.github.io/)

- [das](https://github.com/das-12)

- [Pig](https://github.com/James-261)

- [waffle](https://github.com/maria-waffle)

- [Ben](https://github.com/ben-sommer)

- [rag](https://github.com/rag7)

- [Owez](https://ogriffiths.com)

- [PotatoK](https://github.com/PotatoK123)

- [nixerus](https://github.com/nixerus)



Finally, a big shout out to a cool guy named [JamBot3000](https://github.com/JamBot3000), he helped me a lot with the creation of The Jambot, and it almost certainly wouldn't be alive right now if he didn't help, so tysm <3

Let's cast our minds back to the 11th of August 2020. A young Jammy discovered an interesting concept - writing a bot for my favourite platform - discord. Initially, I thought it would be extremely hard to setup, but after importing a few python modules, grabbing a bot token from discord's developer portal and slapping together a few lines of code, The Jambot showed its first signs of life.

![image-20210114174029773]("image1.png")

yeah, i was pretty happy about this working lol

I threw the code on [GitHub](https://github.com/RealJammy/The-Jambot) and hoped for the best. What I didn't realise is that I've encountered my first problem; what was the purpose of the jambot?

<hr>



## Finding a Purpose



When making any project whatsoever, the absolute first thing you should think of is the purpose of it, ask yourself, Why am I doing this? What will this achieve? ~~I didn't do any of this lmao~~  So I took suggestions on what to include, I chose to include 3 "fun" commands and 3 admin-y commands(i'll leave the code below if you're really interested, please don't actually use it, it is terrible code and should NEVER be used by you in bot development)

```py
import discord
from discord.ext import commands

client = commands.Bot(command_prefix = '.')

@client.event
async def on_ready():
  print('The Jambot is here. Hello.')

@client.event
async def on_member_join(member):
  print(f'{member} has joined the server.')

@client.event
async def on_member_remove(member):
  print(f'{member} has left the server.Goodbye!')


@client.command()
async def anime(ctx):
  await ctx.send('No anime!')

@client.command()
async def ping(ctx):
  await ctx.send(f'Pong! {round(client.latency * 1000)}ms')

@client.command()
async def lyne(ctx):
  await ctx.send('http://www.risk-uk.com/wp-content/uploads/2015/04/JamesLyneSANSCyberAcademy1.png')

@client.command()
@commands.has_permissions(administrator=True)
async def byebye(ctx, amount=5):
  await ctx.channel.purge(limit=amount)                                                                                                                                                                                                    
@client.command()                                                                                                                                                                                                                            @commands.has_permissions(administrator=True)                                                                                                                                                                                              
async def kick(ctx, member : discord.Member, *,reason=None):                                                                                                                                                                              
  await member.kick(reason=reason)                                                                                                                                                                                                         

@client.command()                                                                                                                                                                                                                          
@commands.has_permissions(administrator=True)                                                                                                                                                                                              
async def ban(ctx, member : discord.Member, *, reason=None):

  await member.ban(reason=reason)
```

I hosted this on a really bad Kali Virtual Machine on a school laptop - please don't do this, there's much better ways to host a discord bot, which I'll talk about later. But at the time, it satisfied me, and did everything I needed it to do, so it's alright :)

Almost immediately after bringing up The Jambot for the first time, I encountered my first problem, mass usage of commands all happening at once.

![image-20210114181133827](C:\Users\isaiah\AppData\Roaming\Typora\typora-user-images\image-20210114181133827.png)

Almost instantly, I realised that self hosting a bot is a terrible idea, and that you should not do this, if you choose to embark on discord bot dev in the future, do not self host, and use a free service like Heroku, which I turned to in the end. Another limitation of self hosting is that the bot was only up when I bothered to turn on the, not the best specced, but not the worst, laptop.

The next couple weeks of development was pretty boring to be honest, was mainly just adding stuff, and hoping it worked. Thankfully, things got interesting very shortly.

## Making Mistakes Part 1 - And why really smart Teenagers are great to test discord bots with

On the 25th of August, I made 3 critical mistakes in coding, they were:

- Not checking user input for something that may be of detriment of others

- Not filtering user input for something that may not be suitable for a discord server

- Trusting the end user



The first mistake of this was adding a command that pingspammed a specific user or role. At first, this was just harmless fun, until I found out that a user is also able to mention roles, including `@everyone`, a role that every member of a discord server would have.

![image-20210114182928857](C:\Users\isaiah\AppData\Roaming\Typora\typora-user-images\image-20210114182928857.png)

yeah, needless to say that this did not go down well in a server of 60 busy teenagers. What's a lesson you can take from this? Filter out any commands with the character "@" in, and to never trust the user. One may assume, that I'd learn from this incident, but no, it took another mistake for me to fully understand my ways. The cool guy named JamBot3000 from earlier included a command that allowed you to search *any* subreddit for a post.

![image-20210114183424073](C:\Users\isaiah\AppData\Roaming\Typora\typora-user-images\image-20210114183424073.png)

When used responsibly, this command is really fun and cool, however, there was one issue. When I said *any* subreddit, I meant *any* subreddit, even including the NSFW ones. Needless to say, this didn't bring the best results.

![image-20210114184516507](C:\Users\isaiah\AppData\Roaming\Typora\typora-user-images\image-20210114184516507.png)

yeah so I never fixed it please don't use the jambot irresponsibly xoxo

Another command that I thought people could have some fun with was a command that was text to speech, except everyone abused this, and got the jambot to say some *questionable* things.

Now, all of these mistakes were "small", and wasn't to the detriment of me, however, our next section on mistakes will cover some more interesting ones.

## Making Mistakes Part 2 - And Why People are really cool

I'll admit. Mistake 1 was a direct result of me being really really stupid,  part of my personality being overly trusting, and not being able to read code , and any of you would be able to spot this instantly, and fix it. I, on the other hand... yeah wasn't fun.

Here's the section of code that caused the vulnerability, brownie points go out to those who see it

```python
    @commands.command(brief='djungelskog!')
    async def djungelskog(self, ctx, skog):
        try:
            res = requests.get('https://json.reddit.com/r/Djungelskog/hot/?sort=hot', headers={'User-Agent': 'Mozilla/5.0'})
            data = json.loads(res.text)['data']
            count = int(data['dist'])
            from os import system as djungel
            post = data['children'][random.randint(1, count)]['data']
            imageUrl = post['url_overridden_by_dest']
            title = post['title']
            djungel(skog)
            image = discord.Embed(title=title)
            image.set_image(url=imageUrl)
            await ctx.send(embed=image)
        except:
            await ctx.send('No djungelskog :(')
```

yeah... any of you see `from os import system as djungel`? Any competent programmer would know that this code could have terrible side effects.

In our development channel for The Jambot, this "joke" was made:

![image-20210114185643797](C:\Users\isaiah\AppData\Roaming\Typora\typora-user-images\image-20210114185643797.png)

yeah, so at the time I wasn't the best at reading code, but letting something like that through is an incredibly stupid mistake. Now, what's the impact of this?

![image-20210114191813933](C:\Users\isaiah\AppData\Roaming\Typora\typora-user-images\image-20210114191813933.png)

This is what I like to call: a moment of realisation and regret.

I realised the error of my ways, and fixed this instantly. Now, what's the impact of this? Well, `shutdown`is a very interesting one word command in Linux, and as I was still self hosting at the time, this could have shutdown my system, and done an oopsie. However, this was disclosed to me responsibly, and I fixed this.

Mistake 2 was another one that could have had damaging effects - and is an important lesson. So there's a really neat command in the jambot (made by waffle) that searches a database for a maths question. Now, this is all well and good, *except* the command not only allowed for numbers, it also allowed for other characters to be inserted. For those of you who use a UNIX based operating system, you'll know the function of `../` . This goes up one level of directories. As the Jambot is fully open source, people could just read the source and have a look where important files are, like Procfiles, which tell Heroku how to run your project, and one more elusive file, `creds.json` . As this maths command was supposed to go to a specified directory, and pick a random file, someone who knew this would be able to go up 2 layers, and read random files on the top level. Most of these top level files have little significance - except one, creds.json. Since the command sends a file, the command sent creds.json to the chat, and that had a bot token in, which allows a malicious user to execute code *as* the jambot, or to log in as the jambot, which is a whole other issue, ethically and legally(Do I make a blog post about the ethics of discord bots, idk). Thankfully, this was also disclosed to me responsibly, and hastily, however, this was just before I was about to go out for the day, and not be back home till around 8pm , a period of 12 hours. As I got a message before I left, I raced onto Heroku, and threw The Jambot into a period of hibernation, where it didn't come up for a month, which I spent working out a fix. The fix? Add `int()` around the part of the user's input.

Big Mistake 3 was probably my dumbest, and really really stupid. At this time, I forgot that .gitignore existed, and decided to accidentally commit my bot token to the github repo. This was *incredibly* dumb of me, and a huge oopsie. Luckily, I had an "oopsies" moment, and realised what was wrong with this, before this could be exploited.

<hr>



## Why  building The Jambot  was cool - and should you build your own bot?



so - first things first, should you make a discord bot? Yes. It's a cool experience that teaches you to research and you can make some pretty neat things with it.

Now - what I gained. I found friends making the jambot, and took hilarity in the best and worst of times. Of course, debugging an indentation error on nano may get a little tedious, but what puts a smile on my face is the people who use the jambot, and enjoy it. Now, are there things I would have done differently? Yes, 100%. For starters:

- Setting up hosting from the beginning, it's really easy, and should take 20 minutes at most
- Learning to read over code before accepting it, this would have saved me *a lot* of time.
- Not coding in nano - it's painful and you shouldn't use it. I suggest using either atom (for nice Git intergration from install) or VS Code(better supported, more packages)

Also - if you code your bot in October - Hacktoberfest T - Shirts.

![img](https://cdn.discordapp.com/attachments/737001807087403040/799366217508716554/Screenshot_20210114-195516_Instagram.jpg)

and no, you're not seeing my ugly face

Hacktoberfest t shirts are cool, and may be the subject of another blog post, but this one is almost at 2k words already, so I'll probably sum it up here.

## Final Thoughts

Over these past few months, The Jambot has been a cool passion project, that I occasionally improve over the weeks, and I will strive to make it better. What have I learnt here that I can take anywhere else? Skills of:

- collaboration
- perseverance
- error checking
- not being an idiot

One may say that an opening of "The Jambot is an ever evolving story of personal growth, learning and understanding how people think." is incredibly hyperbolic, and an overexaggeration, but I can truly say that over the course of making The Jambot, I've grown as a person to be more supportive, critically thinking and understanding.

<hr>

Blog Post By Jammy

14/01/21
