# duck-pics

This challenge gave me a 'capture.pcapng' file
>got a capture on the chall author while engaging in "personal matters". see what you can find.

I opened the pcapng file in wireshark to see what I could notice

![Wireshark Screenshot](/duck-pic.png)

The first thing I noticed was that the protocal for every packet was USB.  
Based on the challenge description and this, I guessed that the pcap was a keyboard capture  

I decided to search how to analyze a keyboard pcap file.  
The first result I found was [this](https://github.com/TeamRocketIst/ctf-usb-keyboard-parser)  

I followed the steps described:

```
$ tshark -r ./capture.pcapng -Y 'usb.capdata && usb.data_len == 8' -T fields -e usb.capdata > usbPcapData
```

```
$ python usbkeyboard.py usbPcapData
Blog entry #216

Title: The Strange and unsettling Reality ofDucks' Spiral-ShapePenises.

There are some facts you stumvle uppon in life that leave you changed.  I'm not talking about grand revelations like realizing the meaning of existence, but rather those little, often unwanted, tidbits of knowledge that somehow manage to worm theirway into your brain and stay there.  Forever.....  For me, one of thoss facts is this: ducks have spiral-shaped penieses.

Now, before you click away, thinking this is some sort of absurd prank or outlandish clickbait-let me assure yu, this is real. *Too** real, if I may say.  Ducks, those quaint little creatures that waddle by ponds and quack at passersby, have genitalia that corkscrew in way I never thought possible or necessary. The first time I learned about this, my immediate response was a bewildered wh"why?" followed by a slow creeping discomfort that I havn't been able to shake off since.

I suppose the first question we should all ask is, "How did I even come across this information?"  Well, like all unexpected journeys, it began innocently enogh. I was deep into an internet rabbit hole one evening, starting with wholesome videos of duckligs learning to swim. That should have been my cue to stop. But the curiosity machine that is the internet is relentless, and after clicking from one nature documentary to another, I stumbled upon the unsettling fact that male ducks, SPECIFICALL drakes, have penises that are shaped like corkscrews.

At first,  I didn't believe it.  I mean, why would a duck's reproductive organ *nee* to resemble soething you open a bottle of wine??? It felt like one of those quirky, unnecessary adaptations that evolution sometimes comes up with for reasons that no one really asked for. but the more I read  (and I readALOT), the more uncomforatble  I became.  I couldn't stop imagining it.

[CAPSLOCK][CAPSLOCK][CAPSLOCK]magine ducks waddling around, their spiral-shaped anatomy hidden beneath those seeminglt innocent feathers, waiting for just the right moment,  It's bizarrely elaborate for a bird, considering that mst birds don't even *have8* penises.  They make do with something called a cloacal kiss, where their reproductive organs briefly touch. Ducks, on the other hand, went the extra miile with a complex, coiled machanism. It's almost as if nature, in some strange fit of whimsy said, "You know what ducks need?  A penis that looks like a piece of pasta."

But it doesn't stop there. Oh no. As if the spiral shape wasn't unsettling enough, the whole process of duck reproduction is fraught with weirdness and, frankly, bioviolence.  Female ducks, it turns out, evolved a counter-spiral that's rigreproductive tract to fend off unwanted advances, because yes, the duck world is rife with reproductive coercion. That's right-nature designed an entire system where male and female anatomy are *at odds* with each other, spiraling in opposite directtions, all in the name of, wwll, survival?

So now, every time I see a duck floating gracefully across a pong, I cn't help but feel a little uneasy,.  On the surface, they seem calm, composed, and perfectly harmless. But now that I know what's going on beneath thoss features, I can't unsee it. The piral-shped tspiral-shaped truth is always there, lurking in the background. and honestly, it makes my interactions with ducks,,, awkward. I mean, how am I supposed to look at them the same way again?

                                Tenterthefentertheflag.com


bctf{SSteASt0p_s3nd1Ng_m3_DuCK_p1c$}

                I think what makes it particularly uncomforatble is the juxtaposition between the image we have of ducks and this peculiar biological fact.  Ducks are often associated with peaceful, picturesque moments.  You feed them bread crumbs in the park.  You watch them swim in calm, srene pongs. And then there's this SPIRAL PENIS SITUATION* lurking thajust under the surface  (literally and figuratively....).

This revelation has caused me to question a lot of thigs, Is nature inherently weird? Are there more unsettling facts about animals I don't know yet-and do I event  *want* to know? Could  I have gone my whole life without knowing this about ducks, and would I be happier for it?

In the end, there's no real resolution here, no epiphany that wraps this uncomfortable fact into a neat little bow. Ducks have spiral-shaped penises, and that's just how the world works. But even as I sit here writing this, with me words than necessary on a subject I never intended to delve into, I ca't shake the deeling that something has shifted in my understanding of the animal kingdom, nature, and life.

So the next time you see a duck gliding elegantly across a lake, just remember: beneath that calm exterior is a corkscrew of evolutionary weirdness that will haunt you forever.
```
