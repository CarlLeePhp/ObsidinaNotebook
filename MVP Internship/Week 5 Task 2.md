**[http://git.mvp.studio/users/sign_in](http://git.mvp.studio/users/sign_in)**
likunhui@hotmail.com


## Day 01
Got a error when I run `npm run build`.

![[Pasted image 20230717214101.png]]

Searched it, got:
https://stackoverflow.com/questions/69692842/error-message-error0308010cdigital-envelope-routinesunsupported

https://www.freecodecamp.org/news/error-error-0308010c-digital-envelope-routines-unsupported-node-error-solved/

I installed NodeJS 16. The problem looks like be solved.

There is a solution from Q&A:
[Getting Started with the Competition Project in .NET Core 2.2 - Q&A MVP Studio](http://questionhub.mvp.studio/?qa=31411/getting-started-with-the-competition-project-in-net-core-2-2&show=31411#q31411)
## Day 02
Can I just deploy it? As we need ASP.Net Core 2.x.


#### Front-End App
App is running at port xxx. Request data from the port xxxx.
http://localhost:60998/authentication/authentication/signin
http://localhost:60290/profile/profile/isUserAuthenticated



#### Services
The selected ports are stored in the generated Properties/launchSettings.json file and can be modified by the developer.

Identity will be running at the port 60998.
Profile will be running at the port 60290.
Talent will be running at the port 51689.

Azure:
Identity: https://talentservicesidentity20230813180530.azurewebsites.net/
Profile: https://talentservicesprofile20230813182721.azurewebsites.net
Talent: https://talentservicestalent20230813183857.azurewebsites.net

Azure Win:
Identity: https://talentservicesidentity20230813230952.azurewebsites.net
Profile: https://talentservicesprofile20230813225226.azurewebsites.net
Talent: https://talentservicestalent20230813232146.azurewebsites.net

The app: https://talentappwebapp20230814222029.azurewebsites.net


We may need select ISS Express for these 3 services rather than 'Mars.Sevice.XXX'.
I tried Identity, it works.
![[Pasted image 20230722115045.png]]

It works

## Day 03
More Error after login
likunhui@hotmail.com
kuntal2Xi

leekunhui@gmail.com
kuntal2Xi
Type: employer

http://localhost:61771/TalentProfile
Got errors:
Nothing was returned from render.
![[Pasted image 20230722221108.png]]

## Manage Job Page

Structure:
- EmployerManageJob
	- './Employer/ManageJob/ManageJob.jsx'


