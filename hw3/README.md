1/
Website:
https://www.cse135vn.site/

*NOTE for grading:
Please click in the middle of the tab to show all corresponding data of each user session (In database.html)

2/
Team member name:
	Duc Pham
	Trung Tin Vo
	Kim K Nguyen
3/
Ip address: 164.92.144.173
Account for grader:
	grader
	1234
4/
Changes we make to collector.js
	First, use many files to separate out the work (one file to collect static, one file to collect the static, one file to collect the performance, and one file to collect the activity. Then, we import them to one final collector file.
	When we make a post request to send data we collect back from the server, we save everything in the local storage, then try to push it to the server. There are 2 cases:
	1/For static/performance, we only upload the data once, if it is successful, then we stop trying to upload the data, else, we try to reupload from the user's local storage.
	2/For activity data, we use an event queue, each event has each route and the corresponding activity, we try to push data to the server, if it is successful, then we remove the item out of the storage. Else, we keep the event in the user�s local storage and try to reupload later.

