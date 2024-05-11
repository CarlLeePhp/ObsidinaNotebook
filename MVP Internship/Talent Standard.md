## Account Profile
I cannot understand but `http://localhost:61771/TalentProfile` hits Index action.
So, this time it is SPA totally.


Many Errors from those components inside AccountProfile.jsx. Leave a backup here. Delete all contents and put a simple h4 there.

```html
<div className="ui grid">
    <FormItemWrapper title="Linked Accounts" tooltip="Linking to online social networks adds credibility to your profile">
        <SocialMediaLinkedAccount linkedAccounts={this.state.profileData.linkedAccounts} updateProfileData={this.updateWithoutSave} saveProfileData={this.updateAndSaveData} />
    </FormItemWrapper>
    <FormItemWrapper title="User Details" tooltip="Enter your contact details">
        <IndividualDetailSection controlFunc={this.updateForComponentId} details={profile} componentId="contactDetails" />
    </FormItemWrapper>
    <FormItemWrapper title="Address" tooltip="Enter your current address">
        <Address addressData={this.state.profileData.address} updateProfileData={this.updateWithoutSave} saveProfileData={this.updateAndSaveData} />
    </FormItemWrapper>
    <FormItemWrapper title="Nationality" tooltip="Select your nationality">
        <Nationality nationalityData={this.state.profileData.nationality} saveProfileData={this.updateAndSaveData} />
    </FormItemWrapper>
    <FormItemWrapper title="Languages" tooltip="Select languages that you speak">
        <Language languageData={this.state.profileData.languages} updateProfileData={this.updateAndSaveData} />
    </FormItemWrapper>
    <FormItemWrapper title="Skills" tooltip="List your skills">
        <Skill skillData={this.state.profileData.skills} updateProfileData={this.updateAndSaveData} />
    </FormItemWrapper>
    <FormItemWrapper title="Work experience" tooltip="Add your work experience">
        <Experience experienceData={this.state.profileData.experience} updateProfileData={this.updateAndSaveData} />
    </FormItemWrapper>
    <FormItemWrapper title="Education" tooltip="Add your educational background">
        <Education educationData={this.state.profileData.education} updateProfileData={this.updateAndSaveData} />
    </FormItemWrapper>
    <FormItemWrapper title="Certification" tooltip="List your certificates, honors and awards">
        <Certificate certificateData={this.state.profileData.certifications} updateProfileData={this.updateAndSaveData} />
    </FormItemWrapper>
    <FormItemWrapper title="Visa Status" tooltip="What is your current Visa/Citizenship status?">
        <VisaStatus
            visaStatus={this.state.profileData.visaStatus}
            visaExpiryDate={this.state.profileData.visaExpiryDate}
            updateProfileData={this.updateWithoutSave}
            saveProfileData={this.updateAndSaveData}
        />
    </FormItemWrapper>
    <FormItemWrapper title="Status" tooltip="What is your current status in jobseeking?">
        <TalentStatus status={this.state.profileData.jobSeekingStatus} updateProfileData={this.updateWithoutSave} saveProfileData={this.updateAndSaveData} />
    </FormItemWrapper>
    <FormItemWrapper title="Profile Photo" tooltip="Please upload your profile photo" hideSegment={true}>
        <PhotoUpload
            imageId={this.state.profileData.profilePhotoUrl}
            updateProfileData={this.updateWithoutSave}
            savePhotoUrl="http://localhost:60290/profile/profile/updateProfilePhoto"
        />
    </FormItemWrapper>
    <FormItemWrapper title="Profile Video" tooltip="Upload a brief self-introduction video" hideSegment={true}>
        <VideoUpload videoName={this.state.profileData.videoName} updateProfileData={this.updateWithoutSave} saveVideoUrl={"http://localhost:60290/profile/profile/updateTalentVideo"} />
    </FormItemWrapper>
    <FormItemWrapper title="CV" tooltip="Upload your CV. Accepted files are pdf, doc & docx)" hideSegment={true}>
        <CVUpload
            cvName={this.state.profileData.cvName}
            cvUrl={this.state.profileData.cvUrl}
            updateProfileData={this.updateWithoutSave}
            saveCVUrl={"http://localhost:60290/profile/profile/updateTalentCV"}
        />
    </FormItemWrapper>
    <SelfIntroduction
        summary={this.state.profileData.summary}
        description={this.state.profileData.description}
        updateProfileData={this.updateAndSaveData}
        updateWithoutSave={this.updateWithoutSave}
    />
</div>
```


Then I am going to put them back one by one.

Identity: 60098
Profile: 60290
Talent: 51689

#### Individual Detail Section
`profile/ContactDetail.jxs`

CORS Problem:
```
Access to XMLHttpRequest at 'http://localhost:60290/profile/profile/getTalentProfile' from origin 'http://localhost:61771' has been blocked by CORS policy: No 'Access-Control-Allow-Origin' header is present on the requested resource.
```

Only this request has CORS problem. Do not know what's wrong with it.
Then I found it is 500 error.
![[Pasted image 20230910153133.png]]

Then found nothing returned from this method.

```c#
// Talent.Services.Profile/Domain/Sevices/ProfileService.cs
public async Task<TalentProfileViewModel> GetTalentProfile(string Id)
{
    //Your code here;
    throw new NotImplementedException();
}
```

Refer the method after it, GetEmployerProfile.

```c#
// List, like Skills, Languages, needs a new method
// For a User
public List<UserSkill> Skills { get; set; }
public List<UserLanguage> Languages { get; set; }

// But output to TalentProfileViewModel
public List<AddSkillViewModel> Skills { get; set; }
public List<AddLanguageViewModel> Languages { get; set; }

// So we need this method, copy from original code
protected AddSkillViewModel ViewModelFromSkill(UserSkill skill)
{
    return new AddSkillViewModel
    {
        Id = skill.Id,
        Level = skill.ExperienceLevel,
        Name = skill.Skill
    };
}
```


#### Linked Account Component
Refer `IndividualDetailSection` to write `SocialMediaLinkedAccount`.
Refer `UpdateEmployerProfile` to write `UpdateTalentProfile`.

`AddSkillViewModel` back to `UserSkill`.
```c#
protected void UpdateSkillFromView(AddSkillViewModel model, UserSkill original)
{
    original.ExperienceLevel = model.Level;
    original.Skill = model.Name;
}
// If it is a new skill generate a new Id for it firstly.
// Do the same thing for others List, like languages.
```

I believes that `linkedAcctounts` was updated successfully. But cannot used for the state of the component.

**A solution**
Do not initial the state in constructor. But the hook method.
```javascript
constructor(props) {
        super(props);

        this.state = {
            showEditSection: false,
            newLinkedAccounts: { linkedIn: "you did not get it", github: "you did not get it" },
        };
    }

    componentWillReceiveProps(props) {
        if (props.linkedAccounts) {
            this.setState({ newLinkedAccounts: props.linkedAccounts });
        }
    }
```

#### Address Component
Refer `SocialMediaLinkedAccount` for `Address` component.

Import JSON to JS object. The JSON file can be read from a web server.
```js
componentDidMount() {
        fetch("/util/jsonFiles/countries.json")
            .then((response) => response.json())
            .then((json) => {
                let options = [];
                let optionKeys = Object.keys(json);
                optionKeys.forEach((c) => {
                    options.push({ value: c, title: c });
                });
                this.setState({ countries: json, countryOptions: options });
            });
    }
```

How to get a list of property names from an object?
```js
// Create an object:
const person = {
  firstName: "John",
  lastName: "Doe",
  id: 5566,
  fullName: function() {
    return this.firstName + " " + this.lastName;
  }
};

console.log(Object.keys(person))
// output: [firstName, lastName, id, fullName]
```

#### Description
Completed


#### Nationality Component
Completed


#### Language Component
View Model:
```js
// Receive by API
AddLanguageViewModel {
  Name: string,
  Level:string,
  Id: string,
  CurrentUserId: string
}
```

API Model:
```c#
public class UserLanguage : IMongoCommon
{
    [BsonId]
    [BsonRepresentation(BsonType.ObjectId)]
    public string Id { get; set; }
    [BsonRepresentation(BsonType.ObjectId)]
    public string UserId { get; set; }
    public string Language { get; set; }
    public string LanguageLevel { get; set; }
    public bool IsDeleted { get; set; }
}
```

Add new button.
The update talent function can cover CRUD oprations for language. What we need to do is changing that array and update the profile.

#### Skill Component
View Model:
```c#
public class AddSkillViewModel
{
    public string Id { get; set; }
    public string Name { get; set; }
    public string Level { get; set; }
}
```

It is a copy of language component.
#### Work Experience Component
View Model:
```c#
public class ExperienceViewModel
{
    public String Id { get; set; }
    public String Company { get; set; }
    public String Position { get; set; }
    public String Responsibilities { get; set; }
    public DateTime Start { get; set; }
    public DateTime End { get; set; }
}
```

[  ] Copy backend part from Skill.
#### Visa Status
JS date.
```js
if (props.visaExpiryDate !== "") {
	let d = new Date(props.visaExpiryDate);
	let year = d.getFullYear();
	let month = d.getMonth();
	let day = d.getDate();
	this.setState({ visaExpiryDate: year + "-" + month + "-" + day });
}
```

Cannot show the date.
![[Pasted image 20240127230349.png]]

#### Job Seeking Status


#### Profile Photo


## Summary
#### Hide and Show
```jsx
// way 1
{this.state.showEdit && <div></div>}

// way 2
<div hidden={!this.state.showEdit}></div>
```


#### Date



#### Grid System
