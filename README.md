# picoCTF_WebGauntlet
<p align="center"><b>Write up for the CTF WebGauntlet from PicoCTF</b></p>
<br/>
<br/>
<br/>
<br/>

<p align="center">- In this Write Up, I'll guide you through how I got to the end of the WebGauntlet CTF</p>
<br/>
<br/>
<br/>
<br/>
<details>
  <summary> <h1> Introduction to the Web Gauntlet CTF </h1> </summary>
  
  ![Introduction to the CTF](https://i.imgur.com/pYW7GTM.png)
  <br/> 
>In the introduction, they question if we can beat the filters of the SQL Injection <br/>
>Don't worry, this looks easier than it looks! <br/>
>One of the tips points that we should look at the *raw hex* in the response<p style="color:red"><i>Oooooh Spooky</i></p>
>Dont worry, we don't need to look into that, all you need is SQL knowledge
</details>
<br/>
<br/>
<br/>
<details>
  <summary> <h1> Looking at the Vulnerable Gauntlet </h1> </summary>
  
  ![The Website](https://i.imgur.com/R3h71uU.png) <br/>
  >Here we have a look at how the website looks, it's a simple Login and Password prompt input
  <br/>
  
  ![Filters](https://i.imgur.com/3w2yjO8.png) <br/>
  >This is the filter php, here we have our limitations to the SQL Injection
</details>
<br/>
<br/>
<br/>
<details>
  <summary> <h1> Round 1 </h1> </summary>
  
  >Let's start with the basics, let's input admin for user, *since that's is what we're given*, and put anything in the password
  
  ![Test 1](https://i.imgur.com/BrjIZ72.png)
  <br/>
  
  >**Look! There's our exploit!** </br>
  >It's injecting the RAW input into the SQL </br>
  >In SQL you can close search string with the special character: > **'** < </br>
  >When you close a SQL string, you can input SQL codes into the system, tricking it to execute your commands </br>
  >That's **SQLi** </br>
  >**Let's try it!**
  <br/>
  
  ![Test 2](https://i.imgur.com/5b6e197.png)
  <br/>
  
  >As we tested, it looks like it's executing it normally, but we don't have the **password**<br/>
  >Let's think, we need to make the System to think we don't need a password!<br/>
  >Let's input ***admin';***<br/>
  >Like any programming, *almost any*, the semicolon ends the line of code<br/>
  >This way we can end the SQL line and ask only the Username, without veryfing the password <br/>
  
  ![Test 3](https://i.imgur.com/a6rFChu.png)
  <br/>
  
  ![Success 1](https://i.imgur.com/3hFFPpj.png)
  <br/>
  
 >**We did it!**<br/>
 >The system actually did read our injection and now verifies only the Username!<br/>
  </details>
    <br/>
<br/>
<br/>
  <details>
  <summary> <h1> Round 2 and 3 </h1> </summary>
  
  >In this part we can follow the same proccess as Round 1<br/>
  >Taking a look at the filters, they don't seem to include our escape strings<br/>
  
  ![Filter 2](https://i.imgur.com/s4Qi8MO.png)
  <br/>
  
  ![Filter 3](https://i.imgur.com/5lhykz8.png)
  <br/>
  
  >But as soon we pass Round 3, *something* happens<br/>
  
 </details>
    <br/>
<br/>
<br/>
<details>
  <summary> <h1> Round 4 (and 5) </h1> </summary>
  >Let's try inputing the admin'; again <br/>
  
  ![Round 4](https://i.imgur.com/ihAXXPE.png)
  <br/>
  
  >***Nothing happened!*** <br/>
  >Let's take a look at the filters
  
  ![Filter 4](https://i.imgur.com/rpXHsbN.png)
  <br/>
  
  >Hmmm, looks like the admin itself is filtered!
  >This took me about 4 hours, I was trying to junction adm + in  but I was using the wrong parammeter<br/>
  >In this website I found my answer
  <a href="https://www.netsparker.com/blog/web-security/sql-injection-cheat-sheet/">Sql Injection Cheat Sheet</a><br/>
  >The SQL String Parammeter I needed was " ***||*** " and not "+"<br/>
  >This might be a bit confusing for new users, but the Database is different, it varies, so we need to study the database to understand what works and what not<br/>
  >This one uses ***SQLite***<br/>
  
  ![Solution 4](https://i.imgur.com/nPhAbrT.png)
  <br/>
  
  >***Let's try it out!***
  
  ![Round 5](https://i.imgur.com/wV0KZp9.png) <br/>
  
  >***It worked!*** <br/>
  >Now let's take a look at the filters <br/>
  
  ![Filters 5](https://i.imgur.com/ysn4EsQ.png) <br/>
  
  >For our own luck, the *UNION* command was added, but we don't use that at all!<br/>
  >Let's do it again!<br/>
  
  ![Win](https://i.imgur.com/ywBbAkY.png) <br/>
  
  >***We did it!***<br/>
  >Let's check out the Filter.php page! <br/>
  
  ![The Flag!](https://i.imgur.com/NkzRTUG.png) <br/>
  
  >Taking a look at the php source code, we can understand a little bit better how it works</br>
  >Our Flag is commented at the end of the code!</br>
  >The tag is ***picoCTF{y0u_m4d3_1t_a5f58d5564fce237fbcc978af033c11b}***

 
