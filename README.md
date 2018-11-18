# Week 8 Project - Pentesting Live Targets

Time spent: 6 hours

> Objective: Exploit vulnerabilities in three different versions of the Globitek website: blue, green, and red.

The six possible exploits are:

- Username Enumeration
- Insecure Direct Object Reference (IDOR)
- SQL Injection (SQLi)
- Cross-Site Scripting (XSS)
- Cross-Site Request Forgery (CSRF)
- Session Hijacking/Fixation

Each version of the site has been given two of the six vulnerabilities. (In other words, all six of the exploits should be assignable to one of the sites.)


## Blue:
### Vulnerability 1: Session Hijacking/Fixation

#### Steps to recreate:
- In one browser (Chrome), we logged in normally but then copied the current PHPSESSIONID by going [here](https://104.198.208.81/green/public/hacktools/change_session_id.php). 
- Use another browser (Safari in this case) which was NOT logged in and change the [PHPSESSIONID](https://104.198.208.81/green/public/hacktools/change_session_id.php) we got from Chrome.
- It will show that it was automatically logged into the system in the Safari without entering the password and username.

![](blue-exploit-1.gif)

### Vulnerability 2: SQL Injection

#### Steps to recreate:
- Go to the salesperson tab
- Select a random salesperson and add this at the end of the url ` ' OR SLEEP(5)=0--'  `

![](blue-exploit-2.gif)


## Red:
### Vulnerability 1: User Enumeration 

#### Steps to recreate:
- Log in and then go to sales person's page
- Click into any salesperson to get their ID and change it to 11 or 12; these information shouldn't be public to everyone
- Log out and go to the public site
- Click into any salesperson and change their ID to 11 or 12 and you will get that information when public user shouldn't supposed to

![](red-exploit-1.gif)

### Vulnerability 2: Cross-Site Request Forgery (CSRF)

#### Steps to recreate:
- Create a html page with the code below
- User submit a feedback with a url that links to the html page
- Admin log into site and visit the attached feedback url
- By visiting the page, it will attack and change salesperson with the ID 5's info 

```
<html>
  <head>
    <title>A Totally Blank Page</title>
  </head>
  <body onload="document.CSRF.submit()">
	<form action="https://104.198.208.81/red/public/staff/salespeople/edit.php?id=5" method="post" style="display: none;" name='CSRF' target="res">
	    <input type="text" name="first_name" value="HACKED" />
      	<input type="text" name="last_name" value="WAS HACKED" />
      	<input type="text" name="phone" value="111-111-2222" />
      	<input type="text" name="email" value="HACKED@HACKED.com" />
	</form>
    <iframe name="res" style="display: none;"></iframe>
  </body>
</html> 
```

![](red-exploit-2.gif)


## Green:
### Vulnerability 1: Cross-Site Scripting (XSS)

#### Steps to recreate:
- Go to Contact section and submit a feedback with `<script>alert('XSS ALERT');</script>`
- Log into admin and once you click the feedback section, it will trigger a popup

![](green-exploit-1.gif)

### Vulnerability 2: Cross-Site Scripting (XSS)

#### Steps to recreate:

- Go to log in page, if you enter the correct username, but inccorect password, `Log in was unsuccessful` will be bolded
- If you enter an invalid username and incorrect password, it wouldn't be bolded.

![](green-exploit-2.gif)

