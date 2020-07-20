# Search Github

## Overview
Explore Github user's by searching for any user to discover their repositories and corresponding branches.

When you first enter the site, start searching for a Github user in the search box. Clicking a user will display their avatar, name and when they joined Github. Underneath is a list of their repositories (a maximum of 100). Respositories have been listed in reverse chronological order and paginated with 25 repositories per page. Clicking on any of the repositories will take you to a list of of all the branches that have been made on that repository.

## Project setup
To run this application locally fork and clone this repository. Then install dependencies by running:
```
npm install
```

Run server and view project at localhost:8080
```
npm run serve
```

## Application Design
This application has been made using Vue.js and Typescript with class components. The styling was done with Vuetify. It has been divided into several components to try and align to the Single Reponsibility principle, with each component having one responsibilty.

The components consist of:
- searchGithub: The main component that's responsibility is to render the child components and pass them appropriate data
- welcome: Displayed when the site is first loaded (or refreshed) and helps user get oriented with the site
- searchUsers: Contains the search bar with autocomplete feature
- selectedUsers: Displays the selected users' information
- repoList: Container for repoListItems and pageNavigation
- repoListItem: Displays a repository and when the repository was created. Plus contains a click event emitter to let searchGithub know if repository is selected
- pageNavigation: This displays page x of y and contains the buttons next and previous to move between repositorty pages 
- branchList: Container for branchListItems and contains a back button to allow users to return to the respository list
- branchListItem: Displays each branch name

## Future improvements
- Setup routing in project
- Improve the search users feature: 
    - by adding user avatars to the autocomplete results
    - Exploring ways to increase performance (is there a way to reduce the number of api calls made?)
- Add more information from Github such as commits to increase the ability for users to explore Github using this application
- Add unit tesing to application
- Add a logo and favicon
- As I continue to learn more about Vue.js, Typescript and Vuetify make improvements to the quality of the code.
