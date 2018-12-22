<h1>LOL-X-Assistant</h1>
<p>Your personal assistant for League of Legends!</p>
<p>Before game start, you don't need to search runes for your champion on the internet anymore; you don't need to click runes icon one by one anymore. The only thing you need to do is run this program, and click once. All the thing you need will be set automatically</p>

<h2>Futures</h2>
<ul>
  <li>Champion Information Displayed</li>
  <li>Spell Information Displayed</li>
  <li>Get Runes For Your Champion Automatically</li>
  <li>Set Runes In One Second For Your Champion</li>
  <li>(Comming Soon)Runes Win Rate Display</li>
  <li>(Comming Soon)Send Champion Win Rate To Your Teammate</li>
  <li>(Comming Soon)Get Your Teammate Champion Win Rate</li>
  <li>(Comming Soon)In-game Timing</li>
  <li>(Considering)Send Your Position Automatically In Blind Pick</li>
</ul>


<p>This program is to make your league of legends experience more comfortable, and is <a href="https://www.reddit.com/r/leagueoflegends/comments/7q6xku/runesreformed_set_your_runes_automatically/dsnjm0z/">allowed by RIOT</a>.</p>

<br>
<br>
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
<p>Now, it clearly shows that [EDI(0x092F15F8)+48C] is the address we want, so let's check:</p>
<img src="https://github.com/xuan32546/LOL-X-Assistant/blob/master/pics/4.png">
<p>So if we can get the value of EDI, we can get our address. But suddenly, I found that we only need to get the value of EAX, we can also get what we want. So let's check:</p>
<img src="https://github.com/xuan32546/LOL-X-Assistant/blob/master/pics/5.png">
<p>Converting to decimal, EAX is what we want. Now, we need to hook this line(MOV [EDI+0x48C],[EAX]), making it to run our codes. However, there is only 6 bytes for us to use, because we cannot affect other codes:</p>
<img src="https://github.com/xuan32546/LOL-X-Assistant/blob/master/pics/6.png">
<p>So what we are going to do is to hook and detour:</p>
<img src="https://github.com/xuan32546/LOL-X-Assistant/blob/master/pics/7.png">
<p>Source Code:  <a href="https://whatis.techtarget.com/definition/base-address">dllmain.cpp</a>. If you inject the dll into the program, the assembly instructions is going to be like this:</p>
<img src="https://github.com/xuan32546/LOL-X-Assistant/blob/master/pics/11.png">
<img src="https://github.com/xuan32546/LOL-X-Assistant/blob/master/pics/8.png">
<img src="https://github.com/xuan32546/LOL-X-Assistant/blob/master/pics/9.png">
<img src="https://github.com/xuan32546/LOL-X-Assistant/blob/master/pics/10.png">
<p>Now, whenever the championId is changed, it will be stored in the variable "championCode" automatically. You can use <a href="https://en.wikipedia.org/wiki/Clipboard_(computing)">Clipboard</a>, <a href="https://en.wikipedia.org/wiki/Shared_memory">Shared memory</a>, <a href="https://docs.microsoft.com/en-us/windows/desktop/winsock/windows-sockets-start-page-2">socket</a>, or some other ways to send data to your program from this injected dll.</p>
<h4>However, the method above may be regard as violation of game security in the future, so thanks for Fumi's help, I switch to RIOT's in-game api to get champion ID. Although I abandoned the method, I think the process of solving a problem is quite attracting, which exactly makes the computer world thrilling and interesting. <a href="https://github.com/Fumi24/RunesReformed">Fumi's Github</a></h4>

