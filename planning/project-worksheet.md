# **<p align="center">Plantr</p>**

# Project Overview

## Project Schedule

|  Day | Deliverable | Status
|---|---| ---|
|Day 1| Project Description | Complete
|Day 1| Wireframes / Priority Matrix / Timeline `backend` and `frontend`| Complete
|Day 2| Working RestAPI | Complete
|Day 3| Core Application Structure (HTML, CSS, etc.) | Complete
|Day 4| MVP & Bug Fixes | Complete
|Day 5| Final Touches and Present | Incomplete

## Project Description

A simple dashboard for making sure your plants are getting the care they need. The preliminary version of Plantr allows you to track whether your plants have been watered.

## Google Sheet

https://docs.google.com/spreadsheets/d/1MiYUM5Rr0hr_9kbYVNgYzxu88jngsMA9udl1Ox-z7Vw/edit#gid=0

## Wireframes

Upload images of wireframe to cloudinary and add the link here with a description of the specific wireframe. Do not include the actual image and have it render on the page.  

- [Mobile](https://res.cloudinary.com/jcloud3zf/image/upload/v1600001397/project-4/plantr-mobile_q8yfnw.png)
- [Desktop](https://res.cloudinary.com/jcloud3zf/image/upload/v1600001379/project-4/p4-desktop_crum2i.png)

## Time/Priority Matrix 

- [Matrix](https://res.cloudinary.com/jcloud3zf/image/upload/v1600083018/project-4/p4-frontend-matrix_zrb0m4.png)

#### MVP (examples)

- Registration is required in order to utilize this API
- Once logged in the user is presented with a dashboard that has a sidebar containing the categories they've registered as well
as a list of plants within those categories
- In order to begin tracking plants the user will need to create a category and add the desired plant to it
- Registration of categories begins in the sidebar, a modal will open up that allows the user to create a new category if they wish
- Once a category is created the main page will display a button allowing a user to add a plant
- Plants have a name, description, as well as a required category that can be defined
- Once a plant is created its information is displayed on the page along with tracking details


#### PostMVP 


- Functionality that allows tracking of ambient temperature and amount of light recieved
- Search bar for plants where needs have not been met
- Allow user to choose color for categories
- Categories are highlighted on click
- Notification when plant need isn't met

## Functional Components

- Hamburger menu, navigation bar, side bar with categories
- Buttons generated for user defined categories, attach to create category request
- Button for adding a new plant within a category
- Display cards for plants in category, using get all plants by category request
- Add new category/delete category button, attach to create/delete category request. Located in sidebar
- Modal popup when creating new category or deleting a category
- Modal popup when adding a new plant to the category. Calls create plant request
- Logout button on navbar

#### MVP
| Component | Priority | Estimated Time | Time Invetsted | Actual Time |
| --- | :---: |  :---: | :---: | :---: |
| Hamburger/Navigation | H | 1hr | 1hr | 1hr|
| List created categories | H | 1.5hr | 1hr | 1hr|
| List created plants | H | 1.5 hr | 2hr | 2hr|
| List plant by category | H | 2 hr| 1.5hr | 1.5hr |
| Display card for plant | H | 1hr | 1.5hr | 1.5hr|
| Conntect buttons to requests | H | 3hrs| 3.4hr | 3.4hr |
| category modal | H | 2hr | 3hr | 3hr|
| plant modal | H | 2hr | 1.4hr | 1.4hr|
| Login page | H | 4hr | 5hr | 5hr |
| side bar | H | 2 hr | 3hr | 3hr |
| responsive | H | 3 hr | 3hr | 3hr |
| vue research| H | 10hr | 9hr | 9hr |
| Total | H | 33 hrs| 34.8hrs | 34.8hrs |

#### PostMVP
| Component | Priority | Estimated Time | Time Invetsted | Actual Time |
| --- | :---: |  :---: | :---: | :---: |
| Notifications | H | 4hr | - | - |
| Category colors | L | 4hr | - | - |
| Category highlight | M | 2hr | - | -| 
| Additional tracking | H | 6 hr | - | - |
| Total | H | 16 hrs| -hrs | -hrs |

## Additional Libraries
VueJS/Vue CLI  
Bootstrap
vue-breakpoints


## Code Snippet

Use this section to include a brief code snippet of functionality that you are proud of an a brief description  

This piece of code allows the user to remain logged in even after refreshing the page. 
Vue instances will be reloaded but they will use the token that is in localStorage

```javascript
beforeMount: function() {
	this.token = localStorage.getItem('data')
}
```

## Issues and Resolutions

**ERROR**: Property or method "expandOnHover" is not defined on the instance but referenced during render
**RESOLUTION**: click events don't work on vue components, instead i needed to use v-on:click.native to get an event to trigger

