## Adding Tailwind CSS to Create-React-App (CRA)

# Tailwind CSS
Tailwind isn’t the first utility CSS library, but it's quite becoming the most popular one in recent times. According to documentation,  [Tailwind CSS](https://tailwindcss.com/)  is a utility-first CSS framework for rapidly building custom designs. 

> Tailwind CSS is a highly customizable, low-level CSS framework that gives you all of the building blocks you need to build bespoke designs without any annoying opinionated styles you have to fight to override.

## Getting Started
You can start along  [CDN](https://tailwindcss.com/docs/installation#using-tailwind-via-cdn)  path, by adding the link to html file. But, you will miss out of many features it has to offer, including customization and third party plugin installations. 

Since this is scripted particularly for Create-React-App not included in its  [official documentation](https://tailwindcss.com/docs/installation) , let us take the npm path.  

### 1. Install via NPM
After installing CRA via ```npx create-react-app <project-name>``` , 

Add tailwind, postcss-cli and autoprefixer for all your styles
```
npm install --save-dev tailwindcss postcss-cli autoprefixer 
``` 

### 2. Generate Tailwind configuration file
These files are used to customize tailwind in your project.
```
npx tailwind init
``` 
generates **tailwind.config.js** at root location

### 3. Generate PostCSS configuration files
We will mention the postcss plugins we want to use in your project.

Create a file named **postcss.config.js** at root level and add following lines
```
module.exports = {
    plugins: [
        require('tailwindcss'),
        require('autoprefixer')
    ]
}
``` 
### 4. Adding tailwind directive 
Create a css file (say, **tailwind.css**) at ```src/styles/``` (it can be any location) and add following directives.
```
@tailwind base;
@tailwind components;
@tailwind utilities;
``` 
### 5. And finally, Generate your tailwind css
Open package.json and edit your script statements as below

Your current package.json script looks like this
```
"scripts": {
    "start": "react-scripts start",
    "build": "react-scripts build",
  },
``` 
This will be changed to

```
    # add css:build and css:watch commands for generating the css
    "build:css": "postcss src/styles/tailwind.css -o src/index.css",
    "watch:css": "postcss src/styles/tailwind.css -o src/index.css -w"

    # update start and build with above css generation
    "start": "concurrently \"npm run watch:css\" \"react-scripts start\"",
    "build": "npm run build:css && react-scripts build",
    
``` 
build and watch statements differ by adding a **-w** for watching the changes in the file and reload the css. What it does is tailwindcss directives are complied and updated in index.css file (already available in CRA).

Don't forget to install **concurrently** package (either globally or project-wise as dev dependency), for running multiple commands concurrently. 

```
npm install --save-dev concurrently
``` 
 
And, start your project, **Voila!**

```
npm start
``` 

## Is it worth? 
Tailwind generated huge interest as well as highest satisfaction among the community, as per  [**State of CSS 2019**](https://www.freecodecamp.org/news/the-state-of-css-2019-survey-results-are-live/). It avoids the tiring HTML-CSS switching and have your styles while you write your blocks. 

Yes, I really love it. You should try it too. 

