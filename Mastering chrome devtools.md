
# Mastering chrome devtools

- Chrome generates DOM Tree while parsing our HTML.
- *shortcut* - Clicking ALT + DOM Tree node will open all the child nodes of that particular node
- Esc key press on any tab except console will open a mini console

- We can select material color palettes from the color panel , and can make custom color panels.
- on color swatch we can click on it by pressing shift and it will convert the format  

---
### Editing

- use scroll into view by right clicking on the DOM node to view that item.
- Tooltip will denote the direction of the DOM Node.
- press h key on the dom node to look how website will look without it but it will take it's spacing. Pressing delete will remove it from dom node

- After browser has dealt with all the specificity and finally rendred the page we can look into `Computed` tab in elements and can find which styles are being applied and on clicking arrow it will take us to that css style.
- Also we can see what eventlisteners are being applied to specific dom nodes
- we can drag and drop dom nodes
- We can add break points to specific nodes so we can detect when the dom node changes like on removal , on attributes changing etc
- we can persist our changes `style changes` by going into filesystem tab and adding a folder to workspace. we will be able to change the styles but won't be able to change dom nodes generated if it's not static html.
- we can select a DOM node in elements and then access it in the console with $0 and past elements with $1 etc.

---

### Debugging

- we can use cmd + shift + p to open autocomplete panel by which can access any tabs and its functionalities
- cmd + p will allow us to access all the files available in workspace
- we can add variables to watch in the `watch` tab and it will reflect the variables current value
- Call stack shows how we reached that particular point in code- mostly it will start through an anonymous function call or an event listener
- Scope defines the scope of function and variables it has access to
- Breakpoints shows the number of breakpoints in our workspace.
-  Black boxing is a technique in which you can add scripts whose function invocations will be hidden in call stack. Like Internal function invocations of react / redux which we don't want to debug.
- we can add conditional breakpoints by right clicking on the line number where we want to add a break point. It allows us to enter a an expression which will be evaluated, execution will stop at that breakpoint only when that condition evaluates to true 
- XHR breakpoints allows you to add a string. It checks that if any AJAX Call contains that string in it's url. If it does then execution will stop at that point.

---

### Networking

- Networking tab in the chrome dev-tools follow waterfall model. 
- On the X-axis is the time taken to load the asset.
- Generally first thing that is fetched is the document which loads other scripts.
-  *shortcut* - Press Shift and hover over items in the network tab. The subsequent items which turn green is the initiator for that item and the red ones are which are called by that item. 
- HTTP 1 can at max serve 6 requests at a time. So if any more files are to be served it will be shown in white color which denotes Queuing.
- Then comes stalling which means it is blocked/waiting until the browser sends the request which will be when queue is empty
- Then comes DNS lookup to look for the IP address behind the domain. Like for Google Ads.
- Then time taken for initial connection.
- Request sent / sending is shown in green color
- Content Download/Downloading is denoted by blue color
- We can record the loading of the the page, make sure that chrome dev-tools are undocked to separate window.
---

### Auditing

- Services like Lighthouse , webhint.io gives you a comprehensive list of how your website/web-app performs and gives you insights regarding how you can improve.
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE1NTA0ODA4MDEsMTU0MzE2NDU1MSw1MT
ExMTIxNTYsMTM1MzYzMDg5NCw2NzgyMzE2NTQsNDY4MDc0Mzc2
LC0yNjM5MzM0OTEsLTExMTk2NzcwODYsMTQ5OTQwMzU2OCwxNT
k5NTM1MzA4LC05MzcyNDQyMTQsMzYyNzk1NDM0LDE2OTQyMzI0
MzksLTE5MzkwOTAxMjZdfQ==
-->