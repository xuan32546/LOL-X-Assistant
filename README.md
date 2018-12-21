
<h2>This program is to make your league of legends experience more comfortable, and is <a href="https://www.reddit.com/r/leagueoflegends/comments/7q6xku/runesreformed_set_your_runes_automatically/dsnjm0z/">currently allowed by RIOT</a>.</h2>

<h3>In this article, I will illustrate one interesting way of getting champion name which users are selecting, which is not widely used by others, and there are few tutorials on the internet.</h3>
<p>It's common sense that the champion name corresponds to the champion ID, so what we need to do is to find champion id. Searching for champion id is quite easy, as the picture shows:</p>
<img src="https://github.com/xuan32546/LOL-X-Assistant/blob/master/pics/1.png">
<p>Although I have already found the address of champion ID (0x092F1A84), the value stored in this address will become useless if I restart the program. And when I was learning assembly language on my own, I knew that every data correspond to a <a href="https://whatis.techtarget.com/definition/base-address">base address</a>. So we can use this formula to get champion ID after restarting: BASEADDRESS + OFFSET = CHAMPIONID's ADDRESS.</p>
<p>That is to say, if we find the base address of champion ID, we can get the champion ID</p>
<h3>However, this article is not going to show how to find the base address, because it is quite onerous to find it for this program. Instead, I want to share one easier way to get champion ID (although I finally abandoned it), which I found for the first time.</h3>
