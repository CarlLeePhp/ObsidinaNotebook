### Tools for Coding

Here are what included in our project.

Most of them are front end technologies. 

The left side are front end technologies. Maybe you do not know this one. It called Vue, a javascript framwork. We use it to bind data, mostly. 

We also searched some server side technologies. These four in the middle, php, a database. And we use a Coumputer Engine from Google Cloud to host our web site, with the Ubuntu Server operate system.

These are tools we used for coding, Visual Studio or Visual Studio Code.



### Features and Functionality

Now let's talk about some features and functionalities. Here we talk about 5 things that we have researched.

[Read them one by one]



#### Sharing code for each page

Here is a typical php file of our web site. We use the include statement to aviod copying the navigation bar and footer to each page. So it is easy to maintain the navigation bar and footer.



#### Event and Attribute

Here is the end part of the signup form. The submit button is only available, when the checkbox is checked.

So we bind a event listener to this checkbox. It will update the attribute of the button.



#### Data bind by Vue

Here is part of our Home page. It is used to get package information.

We use the Vue to bind the datas of input text and modal. With this we could change the content in the web site easily.

We also have researched something about Ajax and use it to get package information.

#### Ajax

/ˈeɪdʒæks/

Ajax is a set of Web Development techniques. With it, Web applications can send and retrieve data from a server without refresh the whole page.

For this case, the btnHandler function send the packageID to a server by the GET method. Then a php file catches the packageID and searches information from a MySQL database. When it get the result, the result is sent back to the function. Then it is shown in the page.



#### Form Validation

Here is an example for form validation in our web site. This function comes from Bootstrap. We just need to set the right type and a required attribute for it.