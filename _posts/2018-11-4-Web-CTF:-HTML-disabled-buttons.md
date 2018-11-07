---
layout: post
title: Web CTF:HTML disabled buttons
published: true
---
The very first web task in Roor-me remind me how bad I am at Web🌚
Here's the [question](https://www.root-me.org/en/Challenges/Web-Client/HTML-disabled-buttons?lang=en&action_solution=voir&debut_affiche_solutions=2#pagination_affiche_solutions)
Open the web, we can see this:
![Screen1.png]({{site.baseurl}}/_posts/Screen1.png)

The input box and the button is disabled. We can see the source code:

![Screen2.png]({{site.baseurl}}/_posts/Screen2.png)

The thing is, we need to remove the disable tag. I thought I cannot change the code directly since it's in the web server. However, when you open the inspector of Firefox, we can change the tag and the box and button will be enabled. 
![Screen3.png]({{site.baseurl}}/_posts/Screen3.png)

Then we can input some in the box and submit it. The page will return the flag:
![Screen4.png]({{site.baseurl}}/_posts/Screen4.png)


Also, we can send the post request directly by python or whatever you want:
```python
import requests // requests module only available in Python >3
// make a POST request with auth-login and authbutton set
r = requests.post('http://challenge01.root-me.org/web-client/ch25/',
    data = {'auth-login':'admin', 'authbutton':'Member+Access'});
// print the server's response
print(r.text);
```
