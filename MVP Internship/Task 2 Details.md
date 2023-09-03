[Competition task · Wiki · talent-competition / Talent Competition · GitLab (mvp.studio)](http://git.mvp.studio/talent-competition/talent-competition/wikis/guides/competition-task)

The main jsx file for this task is `\wwwroot\js\react\ReactScripts\Profile\EmployerProfile.jsx`.

#### Employer Profile Page:
- Add last name to the primary contact details.
- Allow users to edit company contact details by clicking on the edit button.

![[Pasted image 20230723104708.png]]

- Display the user's full name on primary contact details (for read only display)

![[Pasted image 20230723104803.png]]

#### Manage Job Page
1. Add a new job by clicking on 'Post a Job' button
2. Check the Mongo DB database for the newly inserted record (under the Job Collection)
3. Click on Manage Job page (this is the UI to work on)

Display jobs as a list of cards

![[Pasted image 20230723130902.png]]

Bonus/Optional: Update a job, Close a job.

#### Add new Component

Add a new entry in the webpack.config.js file.
```js
entry: {
   accountProfile: './ReactScripts/AccountProfile.js',
   homePage: './ReactScripts/Home.js',
   searchResult: './ReactScripts/SearchResult.js'
},
```