
Site url:
https://reporting.cse135vn.site/

Info for logging in:

Admin account:
username: graderAdmin
email: graderAdmin@cse135.site
password: 123123

Normal account:
username: graderNormal
email: graderNormal@cse135.site
password: 123123

Part 1: Authentication
	In this part, our team use PassportJS to implement authentication because PassportJS is a popular middleware for authentication in Express.
	We use Express route to create routes for user login/signup, and check if the user is still in session and what type of the user is to direct user to other pages + give customize options (such as admin can create user). Also, we implemented for user to login with email or password. 

Part 2:
	NOTICE: We implemented to validate if input is valid before create user (Did not know we do not have to do that). So, please create a user that has username, password, and email that has more than 6 characters.
	You can edit fields such as username, email, admin by click in grid. However, when you try to edit the hashpassword, it won't work even it show successfully update because if we allow admin to edit the hash password, it would be impossible to know what password could be hash to that.
	
Part 3:
	We use a line chart to display the number of session per days to see the frequency our website is visited.
	We use a keyup/down bar chart to show what keys the user usually hit when they go to our website. Also, it shows the frequency when the user press the key and hold for a long time, which makes the key down event greater than the key up
	We use a pie chart to show what is the prefered language of the user.
	Finally, we use a grid to devide the load time in many intervals and check the percentage of that load time in total, such as the load time from 200ms to 400ms takes how many % of all sessions

Part 4:
	In the final part, we are trying to answer the question "Is our load time is good enough?" 
	We use a pie chart to see the distribution of load time 0-200ms, 200ms - 400ms, ..., > 1000ms
	We use a bar chart to show the user idle times and the number of times we do not get load time < 1000ms (It can be useful because if our webpage is slow, the user tend to go to another website and then go back).
	Finally, we use a grid to keep track of the number of the loading time that satisfy "L" in RAIL, calculate the percentage and see our website perfomance.

