
<h2>This program is to make your league of legends experience more comfortable, and is <a href="https://www.reddit.com/r/leagueoflegends/comments/7q6xku/runesreformed_set_your_runes_automatically/dsnjm0z/">currently allowed by RIOT</a>.</h2>

<h3>In this article, I will illustrate one interesting way of getting champion name which users are selecting, which is not widely used by others.</h3>
<p>It's common sense that the champion name corresponds to the champion ID, so what we need to do is to find champion id. Searching for champion id is quite easy, as the picture shows:</p>
<img src="https://github.com/xuan32546/LOL-X-Assistant/blob/master/pics/1.png">
<p>Although I have already found the address of champion ID (0x092F1A84), the value stored in this address will become useless if I restart the program. And when I was learning assembly language on my own, I knew that every data correspond to a <a href="https://whatis.techtarget.com/definition/base-address">base address</a>. So we can use this formula to get champion ID after restarting: BASEADDRESS + OFFSET = CHAMPIONID's ADDRESS.</p>
<p>That is to say, if we find the base address of champion ID, we can get the champion ID, which is widely used nowadays.</p>
<h3>However, this article is not going to show how to find the base address, because it is quite onerous to find it for this program. Instead, I want to share one unique way to get champion ID (although I finally abandoned it).</h3>
<p>At first, I tried to find the base address, but I failed. So after several days trying and failing, I used detouring to get champion ID successfully.</p>
<p>Every time I change the champion, the value of champion ID will change:</p>
<img src="https://github.com/xuan32546/LOL-X-Assistant/blob/master/pics/2.gif">
<p>And the assembly instruction might be MOV [DESTINATION],[VALUE], I thought. At first, I wanted to get the DESTINATION, which might be the address of champion ID, so I checked the assembly instruction which controls champion ID:</p>
<img src="https://github.com/xuan32546/LOL-X-Assistant/blob/master/pics/3.png">
