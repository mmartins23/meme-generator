# Meme Generator

This project is a simple meme generator app built with React. 

The app allows users to generate memes by selecting an image from a list of popular memes, entering custom text for the top and bottom of the meme, and then clicking a button to generate a new meme.

[Launch Live Preview](https://lucky-rugelach-9d52a0.netlify.app/)

## Table of Contents

- [Features](#features)
- [Documentation](#documentation)
- [Installation](#installation)
- [Usage](#usage)
- [License](#license)
- [Contact](#contact)

## Features

The main features of this meme generator project include:

1. A user interface that allows users to input custom text for the top and bottom of a meme, and generate a new meme by clicking a button.

2. Integration with the Imgflip API, which provides a list of popular memes and their associated URLs.

3. Random image generation, which allows users to generate a new meme image at random from the available memes.

4. The ability to customize the text for both the top and bottom of the meme.

5. A simple, intuitive design that is easy to use and understand.

6. The app is built using React, which makes it easy to develop and maintain over time.

The project is open source, which means that anyone can contribute to its development and improvement.

## Documentation

```js
import Header from "./components/Header"
import Meme from "./components/Meme"

export default function App() {
    return (
        <div>
            <Header />
            <Meme />
        </div>
    )
}
```

This code is defining a React component called **`App`**. The **`App`** component is being exported as the default export of the module, which means that it can be imported into other files using **`import App from './App'`**.

The first line of the code imports the **`Header`** component from a file located at **`./components/Header`**. Similarly, the second line of the code imports the **`Meme`** component from a file located at **`./components/Meme`**.

The **`App`** component returns a JSX expression that defines the structure of the component. The structure consists of a **`div`** element that contains the **`Header`** component and the **`Meme`** component. The **`Header`** component will be rendered before the **`Meme`** component in the DOM.

Note that both **`Header`** and **`Meme`** components are being used as self-closing tags, which means they don't have a closing tag. This is allowed in JSX, as long as the component doesn't have any children.

Overall, this code defines a React component that renders a header and a meme component in the DOM, in that order.

***

```js
import React, {useState, useEffect} from "react"

export default function Meme() {
    const [meme, setMeme] = useState({
        topText: "",
        bottomText: "",
        randomImage: "http://i.imgflip.com/1bij.jpg" 
    })
    const [allMemes, setAllMemes] = useState([])
    
    
    useEffect(() => {
        async function getMemes() {
            const res = await fetch("https://api.imgflip.com/get_memes")
            const data = await res.json()
            setAllMemes(data.data.memes)
        }
        getMemes()
    }, [])
    
    function getMemeImage() {
        const randomNumber = Math.floor(Math.random() * allMemes.length)
        const url = allMemes[randomNumber].url
        setMeme(prevMeme => ({
            ...prevMeme,
            randomImage: url
        }))
    }
    
    function handleChange(event) {
        const {name, value} = event.target
        setMeme(prevMeme => ({
            ...prevMeme,
            [name]: value
        }))
    }
    
    return (
        <main>
            <div className="form">
                <input 
                    type="text"
                    placeholder="Top text"
                    className="form--input"
                    name="topText"
                    value={meme.topText}
                    onChange={handleChange}
                />
                <input 
                    type="text"
                    placeholder="Bottom text"
                    className="form--input"
                    name="bottomText"
                    value={meme.bottomText}
                    onChange={handleChange}
                />
                <button 
                    className="form--button"
                    onClick={getMemeImage}
                >
                    Get a new meme image 🖼
                </button>
            </div>
            <div className="meme">
                <img src={meme.randomImage} className="meme--image" alt="Random Meme Img"/>
                <h2 className="meme--text top">{meme.topText}</h2>
                <h2 className="meme--text bottom">{meme.bottomText}</h2>
            </div>
        </main>
    )
}
```

This is a React component called **`Meme`**, which is being exported as the default export of the module, allowing it to be imported into other files using **`import Meme from './Meme'`**.

This code uses the **`useState`** and **`useEffect`** hooks from React to manage the component's state and perform side effects respectively.

In the component's state, there are two properties - **`meme`** and **`allMemes`**. **`meme`** contains three properties: **`topText`**, **`bottomText`**, and **`randomImage`**. The **`allMemes`** state property is an empty array that will be filled with data from an external API later on.

The **`useEffect`** hook is used to fetch data from an external API when the component is mounted. The **`async`** function **`getMemes`** is declared inside **`useEffect`**, which fetches data from the URL **`https://api.imgflip.com/get_memes`**. The **`data`** object is extracted from the API response using the **`json`** method, and the **`data.memes`** array is used to set the **`allMemes`** state property.

The **`getMemeImage`** function is used to randomly select an image URL from the **`allMemes`** state array and set it as the **`randomImage`** property in the **`meme`** state object. This function is called when the user clicks on the "Get a new meme image" button.

The **`handleChange`** function is used to update the **`meme`** state object whenever the user types in the "topText" or "bottomText" input fields. This function is called when the user types in either of the input fields.

The **`return`** statement is returning JSX, which is used to render the component on the DOM. The JSX consists of a **`main`** tag containing two divs - a **`form`** and a **`meme`**. The **`form`** div contains two input fields for the user to enter the top and bottom text of the meme, and a button to get a new meme image. The **`meme`** div contains an image tag displaying the random meme image URL, and two **`h2`** tags displaying the top and bottom text entered by the user.

***

```js
export default function Header() {
    return (
        <header className="header">
            <img 
                className="header--image"
                alt="Troll Face"
            />
            <h2 className="header--title">Meme Generator</h2>
            <h4 className="header--project">React Course - Project 3</h4>
        </header>
    )
}
```

This is another React component called **`Header`**, which is also being exported as the default export of the module.

In this component, there is a **`header`** tag with a class name of **`header`**, which contains an **`img`** tag with a class name of **`header--image`** and an **`alt`** attribute set to "Troll Face". This image is commonly associated with internet memes.

Below the image, there are two **`h2`** and **`h4`** tags. The **`h2`** tag has a class name of **`header--title`** and displays the text "Meme Generator", while the **`h4`** tag has a class name of **`header--project`** and displays the text "React Course - Project 3".

This component is used to display a header section on the webpage, which shows the title of the application and the name of the project it was created for.

***
### Summary

1. The first file you have is **`App.js`**. It is the main component that is being exported as the default export of the module. This component renders the **`Header`** and **`Meme`** components inside a **`div`** tag.
2. The **`Meme`** component is defined in the second file, which imports **`React`**, **`useState`** and **`useEffect`** from the **`react`** module. This component sets up two **`useState`** hooks. One for **`meme`**, which is an object with **`topText`**, **`bottomText`**, and **`randomImage`** properties. The second hook is for **`allMemes`**, which is initialized to an empty array.
3. There is an **`useEffect`** hook that is used to fetch data from the Imgflip API. It is called when the component mounts for the first time because the dependency array **`[]`** is empty. The API returns an array of meme objects which is stored in the **`allMemes`** state variable using **`setAllMemes`**.
4. **`getMemeImage`** is a function that is called when the user clicks on the "Get a new meme image 🖼" button. This function uses **`Math.random()`** to generate a random index and selects a random meme from the **`allMemes`** array. The URL of the meme image is then stored in the **`randomImage`** property of the **`meme`** state variable using **`setMeme`**.
5. The **`handleChange`** function is called when the user types in the **`input`** fields for the **`topText`** and **`bottomText`**. It sets the **`topText`** and **`bottomText`** properties of the **`meme`** object in state by using the **`event.target`** object.
6. Finally, the **`Meme`** component returns a **`main`** tag with two child **`div`** tags. The first **`div`** is a form that contains two **`input`** fields for **`topText`** and **`bottomText`** along with a button to generate a new meme image. The second **`div`** is an area to display the meme image along with its top and bottom text.
7. The **`Header`** component is defined in a separate file and exports a simple header section with an image, the title "Meme Generator", and the project name "React Course - Project 3".

In summary, this app uses React to fetch data from an external API, allow the user to modify some text fields, and generate a new meme image with the modified text. It displays the result on the same page using the **`Meme`** component, and the **`Header`** component provides a header section to the page.

## Installation

To install and run this project, follow these steps:

1. Clone the repository: `git clone https://github.com/mmartins23/meme-generator.git`
2. Change into the project directory: `cd example`
3. Install dependencies: `npm install`
4. Run the app: `npm start`

## Usage

To use the app, simply open it in your web browser and follow these steps:

1. Enter text for the top and bottom of the meme in the input fields.
2. Click the "Get a new meme image" button to generate a new meme.
3. Enjoy your new meme!

## License

[![License](https://img.shields.io/badge/license-MIT-blue.svg)](https://opensource.org/licenses/MIT)

This project is licensed under the terms of the MIT license. See [LICENSE](LICENSE) for more information.



## Contact

You can reach me on [Twitter](https://twitter.com/23mmartins)


Feel free to send me a message if you have any questions or feedback about this project. I'll do my best to respond as soon as possible.
