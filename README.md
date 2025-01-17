# Undebate Self Service Portal

In 2019 we created [Undebates](https://github.com/EnCiv/undebate) and launched them in the 2020 primary and general elections. In 2020 we were contacted by the UCLA Student Association who wanted this for their student body elections. We realized there are other organizations that need a way to create undebates for their democratically run elections and so this project creates a portal that allows people to create their own - for example a University Student Body might want to have undebates by the candidates for student body office like president and vice president and such. In the Undebate repo we documented the requirements for a portal for election leaders in this [issue](https://github.com/EnCiv/undebate/issues/301).

## [Example:](https://cc.enciv.org/country:us/organization:ucla-student-accociation/office:usac-president/2021-05-07)

[![image](https://user-images.githubusercontent.com/3317487/133139497-b040d82c-cb7c-46b0-8a2b-e6a44b2ffcd3.png)](https://cc.enciv.org/country:us/organization:ucla-student-accociation/office:usac-president/2021-05-07)

## [Why](https://www.behance.net/gallery/127641633/Self-Service-Portal)

[![image](https://user-images.githubusercontent.com/3317487/139926780-3aa5346c-6108-488e-9d52-54fc6b3e32d0.png)](https://www.behance.net/gallery/127641633/Self-Service-Portal)

**Copyright 2021 EnCiv, Inc.** This work is licensed under the terms described in [LICENSE.txt](https://github.com/EnCiv/undebate/blob/master/LICENSE.txt) which is an MIT license with a Public Good License Condition

# Getting Started

## **Slack** - Use this form to get an invite to the [slack workspace](https://docs.google.com/forms/d/e/1FAIpQLSee58BUiy12dtloG9pLITsELcNldIwXcEtCotV9r95BZJSIVA/viewform)

The following has been tested using node v16.13.0 and npm v8.1.0 on Windows 10 and MacOs. There are known issues using npm < 7. During install, you can ignore the warning about incompatibility with previous versions of node/npm - we need to go back to those packages and update their dependencies. Also, Node version 17 will not work, and in general the odd versions are experimental so we don't try to use those. If you already tried to build this with version 17, you need to install version 16 and then do `npm ci` to start clean.

Below are specific instructions for cloning and running storybook on your local system using your CLI of choice:

```
# Navigate to the local directory where you'd like to clone the project and then issue the following command:
git clone https://github.com/EnCiv/undebate-ssp.git

# Now navigate into the newly cloned project directory:
cd undebate-ssp

# Install the node_module dependencies required to run this project:
npm install

# Now start the project:
npm run storybook
```

A storybook browser window will open up:

![image](https://user-images.githubusercontent.com/3317487/147786004-a6cf5bb9-030a-4011-b0e3-eabc4a1f4c38.png)

Storybook allows us to create React components independently, test them, and leaves a visual catalog of our components for the next contributer. Also, as soon as you get your new component and story started, you can build/edit them on the fly and the browser will update as you make your changes. (Because Storybook uses Webpack to push updates to the browser). 

# Prettier

## If you don't already have [prettier](https://marketplace.visualstudio.com/items?itemName=esbenp.prettier-vscode) for VSC installed, go [here](https://marketplace.visualstudio.com/items?itemName=esbenp.prettier-vscode) and click **Install**.

Prettier makes some spacing and the use of quotes and a few other things consistent across the project. It's really handy when using Visual Studio Code (see below) to be able to just save the file and have the indenting and formatting automatically fixed up. This can help find problems sometimes, and save some of the tedium.

This repo has a .vscode/settings.json file with the basic configuation for using prettier setup for this workspace. It will not override the configuration for other workspaces.
If you are not using VSC, prettier will also be run on the changed files before you commit, but see if prettier is available for your editor and post instuctions here.

# ESLint

## If you don't already have [ESLint](https://marketplace.visualstudio.com/items?itemName=dbaeumer.vscode-eslint) for VSC installed, go [here](https://marketplace.visualstudio.com/items?itemName=dbaeumer.vscode-eslint) and click **Install**.

This project is using ESLint to help prevent bugs. This works really well within the Visual Studio Code environment where it higlights the issues, and can auto fix some of them.

There is no requirement to resolve lint issues, and many that are more preference than bug related have been turned off. If there are rules that we should turn off, or add - its worth discussing. The goal is not to enforce a particular coding style to make it "easier to read", many people work on this project who are experienced with different coding styles. The goal is to prevent bugs. The best coding style is the working code style.

One burden is that if we create new input components, we need to push them to the array in .eslintrc.js/module.exports.rules[jsx-a11y/label-has-associated-control][1].controlComponents

## See the Github **[Issues](https://github.com/EnCiv/undebate-ssp/issues)** for tasks that need doing

-   We are creating React components based on UI design in [figma](https://www.figma.com/proto/IQKPx02pkBErpmhQoECoq9/Undebate?node-id=123%3A1694&scaling=min-zoom&page-id=102%3A2&starting-point-node-id=123%3A1694)

-   For React work, look for issues with a **React** tag.

-   There are also some node and non-rendering client side tasks marked with the **Javascript** tag.

-   Each React component goes into app/components

-   For each component we will also build a story in stories/

-   Here are examples of [components](https://github.com/EnCiv/undebate-ssp/tree/main/app/components) and [stories](https://github.com/EnCiv/undebate-ssp/tree/main/stories)

-   See here for info on the [data schema](https://github.com/EnCiv/undebate-ssp/issues/46)

## Notes on React component guidelines:

These notes are pretty general and always open to reevaluation. Also, we want to state the 'why' for each guideline.

**my-component.js**

```js
// https://github.com/EnCiv/undebate-ssp/issue/NUMBER
import React from 'react'
import { createUseStyles } from 'react-jss'
import cx from 'classnames'

export default function MyComponent( props ) {
    const { className, style } = props
    const classes = useStylesFromThemeFunction(props)

    return (
        <div className={cx(className, classes.wrapper)} style={style}>
            Hello World
        </div>
    )
}

// we want to see the code first, so we put the classes at the bottom
const useStylesFromThemeFunction = createUseStyles( theme => ({
    wrapper: {
        background: theme.colorPrimary,
        padding: '1rem',
    },
}))
```

1. This project is using React-jss for styles, and they should be at the bottom of the file. -- It's efficient to have all the code and style for a component in one place. We've learned over time that we want to see the code first, and then look for the css, so we put the styles at the bottom. We have also started using a theme.

2. The theme is in **app/theme.js**. We should look through there, and add to it as we go, and talk through the best ways to make properties that are common to many components.

3. As in the above example, generally components should accept className and style as parameters, and add those to the outer most element of the component they render. We use `classnames` to combine classes.

4. To make components responsive, do not use 'px'. It's really frustrating that figma shows everthing in px, but we need to convert this to 'rem', 'em', 'vw', or 'vh' as appropriate to make the components responsive. In most of the figma I've seen, a rem is 16px. The only exception to the no 'px' rule is for borders - it's fine to make a border '1px'. But it it gets bigger than that - use rem.

5. Most components should take their width from the parent - not set the width. They should figure out their padding or margin as necessary (in 'rem' usually). Consider that these components are going to run on large screens where the font size is 16 or more and small screens where the font size is 8 or less. There are exceptions.

6. File names should be all lowercase, use '-' between words, and end in .js (.jsx isn't needed). Some OS's are case sensitive others are not.

7. Within the stories.js file for a component, create multiple stories that exercise the functionality of the component. - Future contributors are going to come back to the story to see how the component works - or to test it for some new situation.

8. Include a link to the github issue as a comment at the top of the component file and the top of the story to make it easier to go back and reference it. Also, we should add comments to the issues as we make design decisions that change the original direction in the issue. - We end up putting a lot of good info, and pictures, into the issue and its useful to have it handy even after the issue is closed.

9. Components that accept input, or action from the user should accept an `onDone` parameter, which is a function to call with `{valid: bool, value: any}`. Whenever the user leaves the component, typically through onBlur the component should call onDone, and with value set to the value of this input (which could be an object), and valid set to whether or not the value is valid. Empty should - generally - be considered not valid. Higher level components will figure out how the UI reacts to the valid/value returned. This allows more complete logic than just 'required'.

## Notes on git

When starting to work on a new issue:

```
# Change your local repository's branch to its 'main' branch:
git checkout main

# Pull the current version of project from the gitHub repository and merge it into your local 'main' branch:
git pull

# Create a new local branch (e.g., issue-name#nn) where you will add your changes/fixes and switch to that branch:
git checkout -b issue-name#nn
```

Where `issue-name#nn` is like `election-date-input#7` for issue [#7](https://github.com/EnCiv/undebate-ssp/issues/7)

You don't have to include all the words if it's too long. For example `election-date#7` would be fine too. This makes it easy to find the issue and close it when reviewing the pull request.

After the new component is working great on your local system, you can push it to the github repo under that branch name:

```
git push -u origin issue-name#nn
```

After you've done this once, you can just use:

```
git push
```

to update what's on github.

When the code is ready to merge, go to github.com/EnCiv/undebate-ssp and create a pull request for it. When you go there - there will probably a note at the top asking if you want to create a pull request.

# Icons, Figma and SVG

You can export svg from figma and paste it into a .svg file in assets/svg to create icons. For example assets/svg/trash-can.svg

```
<svg width="24" height="25" viewBox="0 0 24 25" fill="none" xmlns="http://www.w3.org/2000/svg">
<path d="M3 6.58661H5H21" stroke="white" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"/>
<path d="M8 6.58661V4.58661C8 4.05618 8.21071 3.54747 8.58579 3.1724C8.96086 2.79732 9.46957 2.58661 10 2.58661H14C14.5304 2.58661 15.0391 2.79732 15.4142 3.1724C15.7893 3.54747 16 4.05618 16 4.58661V6.58661M19 6.58661V20.5866C19 21.117 18.7893 21.6257 18.4142 22.0008C18.0391 22.3759 17.5304 22.5866 17 22.5866H7C6.46957 22.5866 5.96086 22.3759 5.58579 22.0008C5.21071 21.6257 5 21.117 5 20.5866V6.58661H19Z" stroke="white" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"/>
<path d="M10 11.5866V17.5866" stroke="white" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"/>
<path d="M14 11.5866V17.5866" stroke="white" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"/>
</svg>
```

This project will automatically convert the files in assets/svg into react.js files in app/svgr on install. After you add a new file you can manually trigger the conversion with:

```
npm run svgr
```

Then you can use these svg files as React components in your code like this:

```
import SvgTrashCan from '../svgr/trash-can'

function renderSomething(){
    return <SvgTrashCan />
}
```
